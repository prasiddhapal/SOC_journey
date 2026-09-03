# Module 07 | QRadar Attack Investigation Playbook

## Phase 1: Establish telemetry

1. Review available log sources.
2. Identify IDS and network telemetry.
3. Confirm the internal domain.
4. Identify event and flow sources suitable for correlation.

## Phase 2: Identify suspicious infrastructure

1. Search source and destination IPs.
2. Identify repeated alerts and useful SIDs.
3. Trace communications with suspicious servers.
4. Establish the attacker IP.

## Phase 3: Find the compromised host

1. Pivot from the attacker IP to destination hosts.
2. Identify the first infected system.
3. Review Windows Security activity for the affected host.
4. Identify the employee account.

## Phase 4: Investigate reconnaissance

Search PowerShell and Windows events for:
- Project names
- File searches
- User discovery
- Network discovery
- Security-control checks

In this case, the attacker searched for `project48` and checked PowerShell Script Block Logging.

## Phase 5: Investigate malware

Use Sysmon:
- Event ID 1: process creation
- Event ID 11/15: file activity and hashes
- Event ID 13: registry modification
- Event ID 3: network connections
- Event ID 22: DNS queries

Correlate Process ID, timestamp, user and file path.

## Phase 6: Persistence

Look for:
- `CurrentVersion\Run`
- Startup folders
- Scheduled tasks
- Services
- New privileged accounts

The lab showed a Run Key persistence mechanism mapped to `T1547.001`.

## Phase 7: Account activity

Investigate:
- 4720: account creation
- 4728/4732: privileged group membership
- 4624/4625: successful and failed authentication
- 4672: special privileges

Distinguish legitimate administrative accounts from newly created attacker-controlled accounts.

## Phase 8: Lateral movement and exfiltration

Look for known tools and correlate their execution with:
- Source host
- Destination host
- Account
- Process ID
- Network connection
- File access

The lab showed `wmiexec.py` for lateral movement and `curl` for exfiltration.

## Attack reconstruction

1. Attacker infrastructure was identified through network telemetry.
2. The first infected host was `192.168.10.15`.
3. User `nour` was associated with the compromised endpoint.
4. The attacker searched for `project48`.
5. The attacker checked PowerShell Script Block Logging.
6. `important_instructions.docx` was involved in the initial infection.
7. The malicious file hash was identified.
8. Registry Run Key persistence was established with `T1547.001`.
9. A new account, `rambo`, was created.
10. Process injection activity was linked to PID `7384`.
11. `wmiexec.py` was used for lateral movement.
12. `curl` was used for exfiltration.
13. Host discovery used ICMP against the `192.168.20.0` network.

## Core lesson

A SOC investigation is a correlation problem:

`IP + user + timestamp + Event ID + Process ID + file + registry + network`

The objective is not to collect isolated alerts. The objective is to reconstruct what happened, identify the attacker and explain the evidence chain.
