# Day 34 | Windows Logging, Sysmon & PowerShell Forensics

Practical Windows endpoint investigation using TryHackMe's Windows Logging for SOC room.

## Objectives
- Read Windows Security logs with Event Viewer.
- Investigate 4624/4625 authentication activity.
- Trace 4720/4732 account persistence.
- Use Sysmon Event ID 1 for process analysis.
- Correlate Sysmon 3, 11 and 22.
- Review PowerShell PSReadLine history.

## Investigation model
4625 failed logons -> 4624 successful RDP -> 4720/4732 persistence -> Sysmon 1 -> Sysmon 11/3/22 -> PowerShell history

## Key correlation fields
- Logon ID: authentication/session correlation.
- Process ID: Sysmon event correlation.
- Parent Process ID: process-tree reconstruction.
- Timestamp: attack sequence.

## Lab outcome
Completed manually using Event Viewer, Sysmon logs, file properties and PowerShell history.

## Source
TryHackMe — Windows Logging for SOC.
