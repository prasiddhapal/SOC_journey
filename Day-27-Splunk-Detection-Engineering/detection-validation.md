# Day 27 - Detection Validation

## Objective

Validate the detection with negative and positive tests.

```text
4624 → 4688 → ≤ 300 seconds → Suspicious PowerShell → Detection
```

## 1. Baseline Test

```text
User: Administrator
Source IP: 10.49.108.37
Parent: explorer.exe
Process: powershell.exe
Command: powershell.exe -NoProfile
```

Indicators tested:

```text
encodedcommand | -enc | executionpolicy | download | iex
```

Result:

```text
suspicious = 0
No alert
```

**PASS**

## 2. Process Correlation

```text
explorer.exe → powershell.exe → cmd.exe
PowerShell: 60s after authentication
CMD: 120s after authentication
```

**PASS**

## 3. Source-IP Correlation

The `4688` events lacked a useful `src_ip`. The `4624` event contained `src_ip=10.49.108.37`; `streamstats` carried it forward as `auth_src_ip=10.49.108.37`.

**PASS**

## 4. Time Window

```spl
| eval time_since_auth=_time-auth_time
| where event_id=4688 AND time_since_auth <= 300
```

The 60- and 120-second events were included.

A process beyond 300 seconds was not directly tested.

**PARTIAL**

## 5. Positive Test

```text
User: Administrator
Source IP: 10.49.108.48
Parent: winword.exe
Process: powershell.exe
PID: 5555
Command: powershell.exe -EncodedCommand ABC123
```

Authentication occurred 60 seconds earlier.

Result:

```text
suspicious = 1
parent_risk = 1
risk_score = 5
severity = High
```

**PASS**

## 6. Detection Result

```text
Detection: Suspicious PowerShell After Authentication
Severity: High
User: Administrator
Source IP: 10.49.108.48
Parent: winword.exe
Process: powershell.exe
Command: powershell.exe -EncodedCommand ABC123
Time since authentication: 60 seconds
```

**PASS**

## 7. Validation Matrix

| Test | Expected | Result |
|---|---|---|
| `-NoProfile` | No alert | PASS |
| Suspicious PowerShell without recent auth | No alert | PASS |
| Suspicious PowerShell 60s after auth | High alert | PASS |
| `winword.exe` parent | Risk increase | PASS |
| 300-second boundary | Exclusion test | PARTIAL |

## 8. False-Positive Check

`powershell.exe -NoProfile` returned `suspicious=0`, so PowerShell alone did not generate this alert.

## 9. Limitations

Testing used controlled lab and synthetic events.

Not fully tested: time-boundary cases, legitimate Office-to-PowerShell workflows, larger production datasets, additional PowerShell telemetry, and environment-specific tuning.

## 10. Final Result

```text
Normal PowerShell → No detection

Authentication
      ↓ 60 seconds
Encoded PowerShell
      ↓
High detection
```

**Final status: LAB VALIDATED**

Additional tuning and broader testing are required before production deployment.
