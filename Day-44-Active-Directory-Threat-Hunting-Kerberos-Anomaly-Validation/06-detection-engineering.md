# 06 | Detection Engineering

Potential Kerberos hunting signals:
- abnormal 4769 volume
- unusual account-to-service relationships
- unusual source hosts
- legacy/RC4 encryption in suspicious context
- repeated 4771 failures

Increase confidence with:
- unusual 4624 logons
- 4672 privileged access
- 4688 suspicious processes

Do not alert solely on one 4769, one rare service, one RC4 ticket, or one network logon. Baseline and correlate first.
