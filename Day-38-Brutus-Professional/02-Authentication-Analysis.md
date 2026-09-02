# Authentication Analysis

## Evidence
`auth.log`

## Investigation
Useful commands:

```bash
grep "Failed password" auth.log
grep "Failed password" auth.log | sort | uniq -c | sort -rn
grep "Accepted password" auth.log
grep "Accepted password" auth.log | grep "65.2.161.68"
```

## Findings
Suspicious brute-force source:

`65.2.161.68`

Compromised account:

`root`

A successful authentication was recorded at `Mar 6 06:32:44`.

## SOC Interpretation
Repeated failures followed by successful authentication to a privileged account is a high-priority correlation. The source should be investigated together with subsequent session and command activity.

## Evidence Screenshot
**Evidence 01 - SSH Brute Force and Successful Root Authentication**
