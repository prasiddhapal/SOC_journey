# Day 27 - Findings

## 1. Executive Summary

During today's Splunk session, we built and validated a Windows process-activity detection workflow using authentication (`4624`) and process creation (`4688`) events.

The investigation established a normal process chain:

```text
explorer.exe
    |
    v
powershell.exe -NoProfile
    |
    v
cmd.exe /c whoami
```

The activity was associated with the `Administrator` user and the lab source IP `10.49.108.37`.

The initial activity was assessed as **potentially interesting discovery activity**, but the available evidence did not show strong malicious PowerShell indicators.

A separate controlled test was then created with an encoded PowerShell command launched by `winword.exe`. That test correctly triggered the detection:

```text
Detection: Suspicious PowerShell After Authentication
Severity: High
```

---

## 2. Finding: Authentication Followed by Process Creation

### Evidence

The lab contained:

```text
Authentication
Event ID: 4624
User: Administrator
Source IP: 10.49.108.37
Action: successful_logon
Time: 2026-08-14 04:50:00
```

This was followed by:

```text
Process Creation
Event ID: 4688
User: Administrator
Parent: explorer.exe
Process: powershell.exe
PID: 4216
Command: powershell.exe -NoProfile
Time: 2026-08-14 04:51:00
```

and then:

```text
Process Creation
Event ID: 4688
User: Administrator
Parent: powershell.exe
Process: cmd.exe
PID: 4332
Command: cmd.exe /c whoami
Time: 2026-08-14 04:52:00
```

### Timeline

```text
04:50  Authentication
       Administrator
       10.49.108.37
          |
          | 60 seconds
          v
04:51  explorer.exe -> powershell.exe
       powershell.exe -NoProfile
          |
          | 60 seconds
          v
04:52  powershell.exe -> cmd.exe
       cmd.exe /c whoami
```

### Assessment

The activity is consistent with administrative or discovery activity in the lab.

The `whoami` command is a discovery command, but the PowerShell process itself used only:

```text
-NoProfile
```

No encoded command, `-enc`, `ExecutionPolicy`, download, or `iex` indicator was present in this baseline activity.

**Disposition:**

```text
Benign / Insufficient Evidence
Severity: Low
```

---

## 3. Finding: Process Chain Analysis

The process relationship was reconstructed using the `parent` and `process` fields.

### Observed Chain

```text
explorer.exe
    |
    +--> powershell.exe
            |
            +--> cmd.exe
```

The SPL correlation showed:

| Time | Parent | Process | Command |
|---|---|---|---|
| 04:51 | explorer.exe | powershell.exe | powershell.exe -NoProfile |
| 04:52 | powershell.exe | cmd.exe | cmd.exe /c whoami |

This demonstrated how parent-child process relationships can provide additional context beyond the command line alone.

---

## 4. Finding: Authentication-to-Process Correlation

A five-minute correlation window was implemented.

The key calculation was:

```spl
| eval time_since_auth=_time-auth_time
| where event_id=4688 AND time_since_auth <= 300
```

Observed values in the lab:

```text
powershell.exe -> 60 seconds after authentication
cmd.exe        -> 120 seconds after authentication
```

Both events were therefore inside the five-minute correlation window.

The authentication source IP was carried into the process events as:

```text
auth_src_ip = 10.49.108.37
```

This was important because the original process-creation events did not display `src_ip`. The correlation allowed the authentication source to provide network context for the subsequent process activity.

---

## 5. Finding: Normal PowerShell Detection Test

A baseline PowerShell event was tested:

```text
powershell.exe -NoProfile
```

The detection logic searched for:

```text
encodedcommand
-enc
executionpolicy
download
iex
```

The command did not contain any of these indicators.

Result:

```text
suspicious = 0
```

No suspicious PowerShell alert was generated.

This confirmed that the detection did not automatically classify every PowerShell process as malicious.

---

## 6. Finding: Suspicious PowerShell Test

A controlled test event was created to validate the positive detection path.

### Test Data

```text
User: Administrator
Source IP: 10.49.108.48
Parent: winword.exe
Process: powershell.exe
PID: 5555
Command: powershell.exe -EncodedCommand ABC123
```

The command contained:

```text
EncodedCommand
```

which matched the detection pattern.

The parent process also matched the additional risk condition:

```text
winword.exe
```

### Risk Calculation

The test used:

```spl
| eval risk_score=(suspicious*2)+(parent_risk*3)
```

The resulting values were:

```text
suspicious   = 1
parent_risk  = 1
risk_score   = 5
severity     = High
```

The detection correctly identified the event as:

```text
Suspicious PowerShell After Authentication
```

---

## 7. Positive Detection Result

The final positive test produced:

```text
Detection: Suspicious PowerShell After Authentication
Severity: High
User: Administrator
Source IP: 10.49.108.48
Parent: winword.exe
Process: powershell.exe
PID: 5555
Command: powershell.exe -EncodedCommand ABC123
Time since authentication: 60 seconds
```

This demonstrated that the detection could combine:

```text
Authentication context
        +
Time correlation
        +
PowerShell command-line indicators
        +
Parent-process context
        =
Higher-confidence detection
```

---

## 8. Negative Test Result

A negative test was also performed using the normal lab process:

```text
powershell.exe -NoProfile
```

Result:

```text
No suspicious PowerShell detection
```

Another negative condition occurred when suspicious PowerShell activity was not associated with a recent authentication event inside the five-minute window.

Result:

```text
No alert
```

This demonstrated the value of correlation instead of relying only on a single suspicious string.

---

## 9. Detection Logic Findings

The session established several useful detection-engineering principles.

### Command-line detection

`match()` was used to identify suspicious strings:

```spl
match(lower(command),"encodedcommand|-enc|executionpolicy|download|iex")
```

Using `lower(command)` makes the comparison case-insensitive.

### Event correlation

`streamstats` was used to carry the latest authentication information forward:

```spl
| streamstats current=f last(auth_time_marker) as auth_time last(auth_ip_marker) as auth_src_ip by user
```

### Time-based filtering

The detection restricted process creation to a five-minute window:

```spl
| where event_id=4688 AND time_since_auth <= 300
```

### Analyst output

The final table focused on:

```text
_time
detection
severity
user
auth_src_ip
time_since_auth
parent
process
pid
command
```

This made the result more useful for an analyst than returning the entire raw event.

---

## 10. Important Observation About Source IP

The original `4688` process-creation result did not contain a populated `src_ip` field.

Therefore, a query such as:

```spl
| table _time user src_ip parent process pid command
```

showed an empty source-IP value for the process events.

The solution was to correlate the process creation with the preceding authentication event and carry the authentication source IP forward as:

```text
auth_src_ip
```

For the baseline activity:

```text
auth_src_ip = 10.49.108.37
```

This is a useful lesson when investigating Windows process events: the network-origin field may exist on the authentication event rather than the process-creation event.

---

## 11. Overall Assessment

### Baseline Activity

```text
User: Administrator
Source IP: 10.49.108.37
Process chain: explorer.exe -> powershell.exe -> cmd.exe
Commands:
    powershell.exe -NoProfile
    cmd.exe /c whoami
```

Assessment:

```text
Administrative discovery activity
No strong malicious PowerShell indicators observed
Severity: Low
Disposition: Benign / Insufficient Evidence
```

### Controlled Suspicious Test

```text
User: Administrator
Source IP: 10.49.108.48
Process chain: winword.exe -> powershell.exe
Command: powershell.exe -EncodedCommand ABC123
```

Assessment:

```text
Suspicious PowerShell After Authentication
Severity: High
```

---

## 12. Lessons Learned

1. A process event by itself may not contain the network source IP needed for investigation.
2. Authentication events can provide useful context for subsequent process creation.
3. `streamstats` can correlate ordered events by user.
4. Time-based correlation reduces unrelated matches.
5. PowerShell should not automatically be treated as malicious.
6. Command-line indicators such as `EncodedCommand` provide stronger detection context.
7. Parent-process context can increase confidence in a detection.
8. Positive and negative tests are both necessary before considering a detection reliable.
9. Analyst-facing output should contain the fields required to investigate the alert quickly.
10. The lab detection is a starting point and still requires false-positive tuning before production use.

---

## 13. Final Finding

The Day 27 lab successfully demonstrated a complete detection workflow:

```text
Raw Windows Events
        |
        v
Authentication Context
        |
        v
Process Correlation
        |
        v
Time-Based Filtering
        |
        v
PowerShell Command Analysis
        |
        v
Parent-Process Risk
        |
        v
Severity / Detection
        |
        v
Analyst-Friendly Finding
```

The baseline activity did **not** produce a suspicious PowerShell alert, while the controlled encoded-PowerShell test **did** produce a High-severity detection.

This validates the core detection logic used during today's session.
