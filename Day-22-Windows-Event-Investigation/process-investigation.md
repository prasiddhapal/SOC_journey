# Process Investigation

## Objective

Investigate Windows process creation using Event ID 4688, PID, PPID, parent-child relationships, and command-line telemetry.

## Event ID 4688

Event ID `4688` records the creation of a new process.

Important fields:

- New Process Name
- New Process ID
- Creator Process ID
- Parent Process Name
- Command Line
- User
- Timestamp

## PID vs PPID

```text
PID  → Identifies the process
PPID → Identifies the parent process
```

**Event ID is the event type, not a unique process identifier.**

## Process Relationship

```text
Parent Process
      ↓
Child Process
      ↓
Command Line
```

Example:

```text
WINWORD.EXE
    ↓
powershell.exe
    ↓
update.ps1
```

## Practical Investigation

### WMIC

Observed:

```text
Parent:
C:\Program Files\Amazon\SSM\ssm-agent-worker.exe

Child:
C:\Windows\System32\wbem\WMIC.exe

Command:
wmic.exe computersystem get DNSHostName /value
```

### WmiPrvSE

Observed:

```text
Parent:
C:\Windows\System32\svchost.exe

Child:
C:\Windows\System32\wbem\WmiPrvSE.exe

Command:
wmiprvse.exe -secured -Embedding
```

### TaskHostW

Observed:

```text
Parent:
C:\Windows\System32\svchost.exe

Child:
C:\Windows\System32\taskhostw.exe

Command:
taskhostw.exe NGCKeyPregen
```

## Investigation Rule

A process should not be classified as malicious from its name alone.

Check:

- Parent process
- PID / PPID
- Command line
- User
- Timestamp
- Related processes
- Network activity
- File activity

## Facts vs Hypotheses

```text
FACT:
4688 confirms process creation.

FACT:
PID identifies the new process.

FACT:
PPID / Creator Process ID identifies the process relationship.

HYPOTHESIS:
A process may be related to scheduled-task or system activity.

NOT PROVEN:
The activity is malicious.
```

## Key Lesson

> **Process investigation is about understanding the execution chain, not simply identifying a suspicious-looking filename.**

## Status

**Completed ✅**
