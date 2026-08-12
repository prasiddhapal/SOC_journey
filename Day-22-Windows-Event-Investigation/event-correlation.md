# Windows Event Correlation

## Objective

Correlate Windows authentication and process events to reconstruct activity and build an investigation timeline.

## Core Relationship

```text
4624
  ↓
Logon Session
  ↓
4688
  ↓
Process Creation
  ↓
PID / PPID
  ↓
Command Line
  ↓
Timeline
```

## Logon ID

A **Logon ID** can help correlate events belonging to the same Windows logon session.

Example:

```text
4624
Administrator
Logon ID: 0x72a41d
       ↓
Related events
       ↓
Process / activity
```

A matching Logon ID can provide useful correlation, but it should be combined with timestamps, users, processes, and other telemetry.

## Process Correlation

For Event ID `4688`, correlate:

- New Process
- PID
- Parent Process
- PPID / Creator Process ID
- Command Line
- User
- Timestamp

Example:

```text
svchost.exe
     ↓
taskhostw.exe
     ↓
NGCKeyPregen
```

## Timeline Correlation

```text
Authentication
      ↓
Process Creation
      ↓
Child Process
      ↓
Network / File Activity
      ↓
Additional Events
```

Close timestamps can help establish relationships, but **time proximity alone does not prove causality**.

## Facts vs Hypotheses

```text
FACT:
A 4624 event records successful authentication.

FACT:
A 4688 event records process creation.

FACT:
PID and PPID can establish a process relationship.

HYPOTHESIS:
Two events may be related when their user,
Logon ID, process, and timing support the relationship.

NOT PROVEN:
The activity is malicious without additional evidence.
```

## Investigation Principle

Do not investigate events in isolation.

Correlate:

- User
- Logon ID
- Process
- PID / PPID
- Command Line
- Timestamp
- Network activity
- File activity

## Key Lesson

> **Correlation turns individual Windows events into an investigation timeline.**

## Status

**Completed ✅**
