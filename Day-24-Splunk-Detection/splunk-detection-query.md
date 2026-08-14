# Splunk Detection Query

## Detection Name

Privileged Network Logon Followed by Process Execution

## Objective

Identify a process-creation event that occurs shortly after a successful
network logon and may require further investigation.

## Detection Logic

```text
4624 Successful Logon
        ↓
Logon Type 3
        ↓
Short time interval
        ↓
4688 Process Creation
        ↓
PowerShell / CMD
        ↓
Investigation Required
```

## Lab Telemetry

Observed sequence:

```text
04:50
4624
Administrator
Logon Type 3
Source IP: 10.49.108.37

        ↓ 60 seconds

04:51
4688
powershell.exe
PID: 4216
powershell.exe -NoProfile

        ↓ 60 seconds

04:52
4688
cmd.exe
PID: 4332
cmd.exe /c whoami
```

## Basic Correlation Query

```spl
index=main
| sort _time
| streamstats current=f window=1 last(event_id) as previous_event last(_time) as previous_time
| eval time_diff=_time-previous_time
| eval suspicious=if(
    event_id=4688
    AND previous_event=4624
    AND time_diff<=120,
    1,
    0
)
| table _time event_id user process command previous_event time_diff suspicious
```

## Detection Conditions

The event is marked suspicious when:

```text
Current event = 4688
AND
Previous event = 4624
AND
Time difference <= 120 seconds
```

## Process-Focused Logic

The investigation focuses on command interpreters such as:

```text
powershell.exe
cmd.exe
```

A process-focused condition can be added:

```spl
AND (process="powershell.exe" OR process="cmd.exe")
```

## Example Detection

The lab produced:

```text
04:51
Event ID: 4688
User: Administrator
Process: powershell.exe
Previous Event: 4624
Time Difference: 60 seconds
Suspicious: 1
```

## Why the Detection Is Suspicious

The sequence combines:

- Successful network authentication
- Privileged account context
- Short time interval
- Process creation
- PowerShell execution

This combination provides useful context for analyst investigation.

## False Positives

Potential legitimate explanations include:

- Administrative activity
- IT support
- Remote management
- Automation
- Scheduled tasks
- Administrative scripts

## Analyst Validation

The detection should be validated against:

1. Source IP ownership
2. Account authorization
3. Expected administrative activity
4. Host role
5. Additional process activity
6. Network telemetry
7. Authentication history

## Important Limitation

This detection does **not** prove lateral movement or malicious activity.

A `4624` event followed by `4688` only establishes an observed
authentication/process sequence.

Additional evidence is required before assigning a malicious verdict.

## Severity

**Initial severity: High**

Severity should be adjusted according to:

- Account privilege
- Source reputation
- Host criticality
- Process behavior
- Command-line content
- Supporting telemetry

## Detection Workflow

```text
Windows Telemetry
        ↓
4624 Authentication
        ↓
Correlation
        ↓
4688 Process Creation
        ↓
Process / User / IP Context
        ↓
Detection
        ↓
SOC Investigation
        ↓
Final Assessment
```

## Key Lesson

Detection engineering is not about creating the largest possible number
of alerts.

The objective is to identify meaningful behavioral combinations while
providing enough context for an analyst to investigate them.s
