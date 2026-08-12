# Day 22 - Windows Event Investigation

## Objective

Investigate Windows telemetry using Event Viewer and correlate authentication, process, and system activity.

## Modules

- Event Viewer and Security Logs
- Process Investigation
- Authentication Events
- Event Correlation
- PowerShell Logging
- Windows Investigation Commands

## Practical Work

- Investigated Windows Security events
- Analyzed Event ID 4688 process creation
- Investigated Event ID 4624 successful logons
- Examined PID and PPID relationships
- Built parent-child process relationships
- Correlated Logon IDs
- Identified missing PowerShell 4104 telemetry

## Key Lesson

A single event rarely proves malicious activity.

Effective investigation requires correlating:

- User
- Process
- Parent process
- Command line
- Timestamp
- Logon context
- Network and file activity

## Status

Completed ✅
