# 06 | Detection Engineering

Detection goal: identify suspicious privileged service-account activity while avoiding alerts on normal Kerberos traffic.

Example logic:

4769
AND service-account/SPN targeting
AND unusual source
AND/OR RC4
AND abnormal request volume

Increase confidence when correlated with:
4624 unusual logon
4672 privileged token
4688 suspicious process

Tuning should account for known legacy systems and normal service-account behavior.
