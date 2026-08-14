# Detection Engineering

## Objective

Practice building a basic Splunk detection from Windows authentication
and process-creation telemetry.

## Detection Scenario

The lab telemetry contained:

```text
4624 Successful Logon
        ↓
Administrator
        ↓
10.49.108.37
        ↓
4688 powershell.exe
        ↓
4688 cmd.exe /c whoami
```

The goal was to identify a process-creation event occurring shortly
after a successful network logon.

## Required Telemetry

The detection uses:

- Event ID `4624` - Successful Logon
- Event ID `4688` - Process Creation
- User
- Source IP
- Process
- Parent Process
- PID
- Command Line
- Timestamp

## Detection Logic

Initial logic:

```text
4624
  ↓
Logon Type 3
  ↓
Privileged User
  ↓
Short time interval
  ↓
4688
  ↓
PowerShell / CMD
  ↓
Suspicious Activity
```

The detection is intended to identify activity requiring investigation,
not automatically classify the activity as malicious.

## Basic Correlation

A basic correlation query was developed using `streamstats`:

```spl
index=main
| sort _time
| streamstats current=f window=1 last(event_id) as previous_event
| table _time event_id user process command previous_event
```

This allows the current event to be compared with the previous event.

Example:

```text
4624  → previous_event = -
4688  → previous_event = 4624
4688  → previous_event = 4688
```

## Time Correlation

The time difference between events can be calculated:

```spl
index=main
| sort _time
| streamstats current=f window=1 last(_time) as previous_time
| eval time_diff=_time-previous_time
| table _time event_id previous_time time_diff
```

The lab events showed approximately:

```text
4624 → 4688 = 60 seconds
4688 → 4688 = 60 seconds
```

## Detection Example

A basic detection condition was created using:

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

The logic identifies a process-creation event occurring within
120 seconds of the previous successful logon event.

## Process Filtering

The detection concept can be further restricted to commonly investigated
command interpreters:

```text
powershell.exe
cmd.exe
```

This reduces unnecessary results compared with alerting on every
process-creation event.

## False Positives

Possible legitimate activity includes:

- Administrative automation
- IT administration
- Remote management
- Scheduled tasks
- Administrative scripts

Detection tuning should consider these legitimate use cases.

## Analyst Assessment

The observed sequence is suspicious and requires further investigation.

The available telemetry does not independently prove malicious activity.

Additional investigation should validate:

1. Whether `10.49.108.37` is an authorized host.
2. Whether the `Administrator` account was legitimately used.
3. Whether the activity matches expected administrative behavior.
4. Whether additional process activity occurred.
5. Whether additional network or endpoint telemetry supports the activity.

## Detection Principle

A detection should identify behavior that deserves analyst attention.

It should not automatically be treated as proof of compromise.

```text
Telemetry
    ↓
Detection
    ↓
Alert
    ↓
Investigation
    ↓
Evidence Correlation
    ↓
Final Assessment
```

## Key Lesson

Effective detection engineering requires balancing:

- Detection coverage
- Context
- False positives
- Time correlation
- Process context
- Account context
- Investigation requirements

The goal is not simply to generate more alerts.

The goal is to generate **useful alerts that an analyst can investigate**.
