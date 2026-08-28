# Module 03 | Security Log: User Management

## Important events
| Event ID | Activity |
|---|---|
| 4720 | User created |
| 4722 | User enabled |
| 4723 | Password changed |
| 4724 | Password reset |
| 4725 | User disabled |
| 4726 | User deleted |
| 4732 | Added to local security group |
| 4733 | Removed from local security group |
| 4738 | User changed |

## Investigation workflow
1. Filter for 4720 and 4732.
2. Inspect the Subject.
3. Identify the target account/member.
4. Review time and context.
5. Compare the event Logon ID with the preceding authentication.
6. Identify privileged group membership.

## Lab findings
Backdoor account:
`svc_sysrestore`

Groups:
`Backup Operators`
`Remote Desktop Users`

The Logon ID matched the malicious RDP session.

## Attack chain
4624 successful RDP
-> 4720 account creation
-> 4732 group membership

## Red flags
- Unknown account
- Unusual hours
- Unexpected subject
- Privileged group membership
- Matching suspicious Logon ID
