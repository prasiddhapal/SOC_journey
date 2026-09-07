# Day 43 | Active Directory Monitoring & Kerberos Investigation

Platform: TryHackMe - Monitoring Active Directory
Result: 8/8 tasks | 104 points
Primary tool: Splunk
Status: Complete

## Focus
AD authentication monitoring, Kerberos TGT/TGS telemetry, Windows authentication events, account/group changes, logon baselining, service baselining, and onboarding investigation.

## Verified Results
- Working Splunk index: `win`
- Index discovery: 9,900 events
- Event 4768: 15 TGT requests
- Unique TGT-requesting accounts: 14
- Most common Event 4624 Logon Type: 3
- Most frequent Event 4769 Service_Name: `THM-DC$`
- Computer-account suffix: `$`
- New account: `nathan.brooks`
- Account creator: `adm-luke.sullivan`
- Group: `Marketing`
- Nathan's first TGT source: `10.5.50.12`

## Analyst Takeaway
Baseline normal AD activity before calling an event anomalous. High-volume Kerberos and network logons can be normal. Rare values, unusual sources, timing, account context, and correlated endpoint evidence provide stronger detection signals.

## Evidence Policy
This package contains only screenshots of Splunk commands/queries and their results from the practical investigation. TryHackMe task/instruction screenshots are intentionally excluded.
