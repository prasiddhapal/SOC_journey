# Persistence and Privilege

## Investigation Command
```bash
grep -niE "useradd|adduser|groupadd|usermod" auth.log
```

## Findings
The attacker created:

`cyberjunkie`

The account was subsequently added to:

`sudo`

The log sequence included group creation, user creation and privileged-group membership modification.

## MITRE ATT&CK
**T1136.001 - Create Account: Local Account**

Creating a new local account can provide persistence, particularly when the account is granted administrative privileges.

## Detection Opportunities
Monitor for:
- unexpected `useradd`/`adduser`
- new local groups
- privileged-group changes
- users added to `sudo`
- account creation immediately after suspicious authentication

## Evidence Screenshot
**Evidence 03 - Backdoor Account Creation and Sudo Assignment**
