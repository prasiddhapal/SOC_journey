# 05 | Detection Engineering

Useful Kerberos detection signals include:
- abnormal 4769 volume
- multiple SPN/service-account requests
- unusual source workstation
- legacy/RC4 encryption in suspicious context
- repeated 4771 failures
- unusual 4624 logons
- 4672 privileged logons
- suspicious 4688 process creation

Do not alert on a single event or encryption type alone. Baseline account, host, service, timing and historical behavior first.
