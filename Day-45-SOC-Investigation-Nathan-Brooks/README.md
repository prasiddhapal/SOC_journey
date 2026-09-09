# Day 41 | SOC Investigation - Nathan Brooks

## Objective
Investigate authentication, group membership, SMB share access, file activity, and process telemetry associated with Nathan Brooks and determine whether the observed activity can be confidently classified as malicious.

## Environment
- SIEM: Splunk
- Index: `win`
- Primary hosts: `THM-MKT-WS`, `THM-SHR-SRV`, `THM-DC`
- User: `nathan.brooks` / Nathan Brooks
- Source IP observed for SMB activity: `10.5.50.12`

## Investigation Summary
The investigation correlated Windows authentication, Active Directory group-change, process, and SMB share telemetry. Nathan Brooks was observed in authentication activity and subsequently accessed the `Marketing` SMB share on `THM-SHR-SRV`.

The key file activity was a confirmed SMB `WriteData (or AddFile)` operation against `nathan brooks notes.txt` at approximately `21:20:14` from `10.5.50.12`.

`Notepad.exe` (PID `9048`) was observed on `THM-MKT-WS` shortly before the write operation. However, available telemetry did not directly attribute the network-share write to that process.

A search for direct file-system telemetry using EventCodes `11`, `15`, and `4663` on the file server returned zero events for the target file. Therefore, the exact originating process and malicious intent could not be conclusively established.

## Final Assessment
**Status: Investigation Complete**

**Assessment: Suspicious/Not conclusively malicious.**

Confirmed facts:
- Nathan Brooks performed activity associated with the investigation.
- Source workstation/IP: `THM-MKT-WS` / `10.5.50.12`.
- Destination server: `THM-SHR-SRV`.
- Share: `\\*\\Marketing`.
- File: `nathan brooks notes.txt`.
- EventCode `5145` recorded `WriteData (or AddFile)` at approximately `21:20:14`.
- Additional operations included `READ_CONTROL`, `SYNCHRONIZE`, and `ReadAttributes`; later activity included a `DELETE` operation.
- Direct EventCode `11`, `15`, or `4663` evidence for the target file was not available.

## Key Analyst Lesson
Do not convert temporal correlation into process attribution. The evidence supports a confirmed SMB file operation, but not a confirmed malicious process or confirmed compromise.
