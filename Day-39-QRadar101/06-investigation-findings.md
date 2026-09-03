# Module 06 | Investigation Findings

## Q1-Q24 Answer Summary

| Q | Finding |
|---|---|
| 1 | `15` log sources |
| 2 | `Suricata` |
| 3 | `HACKDEFEND.local` |
| 4 | `192.168.20.20` |
| 5 | SID `2027865` |
| 6 | `192.20.80.25` |
| 7 | `project48` |
| 8 | `192.168.10.15` |
| 9 | `nour` |
| 10 | PowerShell Script Block Logging |
| 11 | `MGNT-01` |
| 12 | `11:14:10` |
| 13 | `9D08221599FCD9D35D11F9CBD6A0DEA3` |
| 14 | `T1547.001` |
| 15 | `icmp` |
| 16 | `office365` |
| 17 | `important_instructions.docx` |
| 18 | `rambo` |
| 19 | `7384` |
| 20 | `wmiexec.py` |
| 21 | `curl` |
| 22 | `Adam` |
| 23 | `192.168.20.0` |
| 24 | `Sami` |

## Key entities

### Attacker
`192.20.80.25`

### First infected host
`192.168.10.15`

### Compromised user
`nour`

### Business target
`project48`

### Malicious file
`important_instructions.docx`

### Malicious file MD5
`9D08221599FCD9D35D11F9CBD6A0DEA3`

### Persistence
`T1547.001`

### New account
`rambo`

### Lateral movement
`wmiexec.py`

### Exfiltration
`curl`

## Defensive interpretation

The strongest evidence came from combining network, Windows Security, Sysmon and PowerShell telemetry. Individual events were useful, but the attack became clear only after correlating identities, hosts, processes, files, registry changes and timestamps.
