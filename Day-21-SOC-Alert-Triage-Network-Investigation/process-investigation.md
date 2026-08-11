# Day 21 - Process Investigation

## Objective

Investigate suspicious process activity using PID, PPID, parent-child relationships, command lines, and endpoint telemetry.

## Process Information

Check:

- Process name
- PID
- PPID
- Parent process
- User
- Host
- Command line
- Executable path
- File activity

## Example

```text
WINWORD.EXE
     ↓
powershell.exe
     ↓
update.ps1
```

A legitimate process can become suspicious because of its **parent-child relationship and execution context**.

## PowerShell Indicators

Investigate commands containing:

```text
-ExecutionPolicy Bypass
-WindowStyle Hidden
-EncodedCommand
```

These indicators require further investigation but do not alone prove compromise.

## Investigation Evidence

For suspicious PowerShell activity, check:

- EDR process creation
- Windows Event ID 4688
- PowerShell Event ID 4104
- Child processes
- File creation
- Network connections
- User privileges

## Key Lesson

> **Do not judge a process by its name alone. Investigate its parent, command line, user, files, network activity, and timeline.**

## Status

**Completed ✅**
