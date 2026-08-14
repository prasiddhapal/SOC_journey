# Investigation Workflow

## Objective

Define a repeatable workflow for investigating suspicious authentication
and process activity identified through Splunk detection logic.

## Investigation Flow

```text
Detection
    ↓
Validate Alert
    ↓
Review Authentication
    ↓
Identify Source
    ↓
Review Process Activity
    ↓
Correlate Timeline
    ↓
Validate Context
    ↓
Assess Risk
```

## 1. Validate the Alert

Confirm that the detection contains the expected telemetry:

- Event ID
- Timestamp
- User
- Source IP
- Process
- Parent Process
- PID
- Command Line

## 2. Review Authentication

For Event ID `4624`, review:

- Account
- Logon Type
- Source IP
- Timestamp

Example:

```text
Event ID: 4624
User: Administrator
Logon Type: 3
Source IP: 10.49.108.37
```

## 3. Review Process Creation

For Event ID `4688`, investigate:

- Process name
- Parent process
- PID
- Command line
- Execution time
- User context

Example process chain:

```text
explorer.exe
      ↓
powershell.exe
      ↓
cmd.exe /c whoami
```

## 4. Correlate the Timeline

Place related events in chronological order.

```text
04:50
4624 - Successful Logon
Administrator
10.49.108.37

        ↓

04:51
4688 - powershell.exe
PID: 4216

        ↓

04:52
4688 - cmd.exe
PID: 4332
```

## 5. Validate Context

Before assigning a malicious verdict, determine:

- Is the source IP authorized?
- Is the account expected to perform the activity?
- Is the host an approved administrative system?
- Could the activity be automation?
- Are there additional related events?

## 6. Assess the Evidence

### Suspicious

Activity that requires additional investigation.

### Malicious

Activity supported by sufficient evidence of compromise or malicious
behavior.

### Benign

Activity supported by evidence showing legitimate expected behavior.

The detection itself should not determine the final verdict.

## 7. Investigation Principle

A single event should not be evaluated in isolation.

Correlate:

```text
User
+
Source IP
+
Authentication
+
Process
+
Parent Process
+
PID
+
Command Line
+
Timeline
```

## Example Assessment

Observed:

```text
4624 Type 3
Administrator
10.49.108.37
        ↓
4688 powershell.exe
        ↓
4688 cmd.exe /c whoami
```

Assessment:

**Suspicious activity requiring further investigation.**

The available telemetry alone is insufficient to conclusively classify
the activity as malicious.

## Recommended Follow-Up

Further investigation should include:

1. Source IP validation
2. Account authorization
3. Additional authentication events
4. Additional process activity
5. Network activity
6. Persistence indicators
7. Endpoint telemetry

## Key Lesson

A good SOC investigation moves from:

```text
Alert
  ↓
Evidence
  ↓
Correlation
  ↓
Context
  ↓
Assessment
```

rather than jumping directly from an alert to a malicious verdict.
