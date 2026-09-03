# Day 39 | QRadar101 Threat Hunting & Attack Reconstruction

Practical SIEM investigation using **IBM QRadar Community Edition** against CyberDefenders' **Qradar101** lab.

## Objectives

- Analyze diverse QRadar log sources.
- Identify the malicious server and attacker infrastructure.
- Correlate Suricata, Zeek and Windows telemetry.
- Investigate compromised Windows hosts and users.
- Trace PowerShell reconnaissance and defense evasion.
- Identify malware, hashes and persistence.
- Reconstruct account creation, process injection, lateral movement and exfiltration.
- Map attacker behavior to MITRE ATT&CK.
- Build an evidence-driven attack timeline.

## Investigation model

QRadar log sources -> network alerts -> attacker IP -> compromised host/user -> PowerShell activity -> malware/file evidence -> persistence -> discovery -> account creation -> process injection -> lateral movement -> exfiltration

## Key correlation fields

- Timestamp: reconstruct attack order.
- Source/Destination IP: identify hosts and communications.
- Username: connect activity to the affected employee.
- Event ID: identify Windows activity.
- Process ID: correlate process execution with follow-on activity.
- Registry path: identify persistence.
- SID / rule name: identify repeated detections.
- File hash: track the malicious file.

## Lab outcome

Completed all **24/24 questions** manually in QRadar.

## High-value evidence

The `Screenshots/` directory contains selected evidence rather than every intermediate screenshot from the investigation.

## Source

CyberDefenders — Qradar101 Lab.
