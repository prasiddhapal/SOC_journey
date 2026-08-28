# Module 02 | Security Log: Authentication

## Core events
| Event ID | Meaning | Use |
|---|---|---|
| 4624 | Successful logon | Identify successful access |
| 4625 | Failed logon | Detect brute force/password spraying |

## Remote logon types
- Type 3: Network logon
- Type 10: Remote Interactive / RDP

## RDP investigation
1. Filter Security logs for 4625.
2. Review Type 3 and Type 10.
3. Look for repeated failures.
4. Check targeted usernames.
5. Check source IPs.
6. Find a later 4624.
7. Save its Logon ID.

## Lab findings
- Brute-force source: `10.10.53.248`
- Compromised account: `Administrator`
- Malicious RDP Logon ID: `0x183C36D`

## Why Logon ID matters
It acts as a session identifier that can connect the initial authentication to later account or process activity.

## Evidence
- 4624 screenshot
- 4625 screenshot
- XML/Details view showing Logon Type and Logon ID
