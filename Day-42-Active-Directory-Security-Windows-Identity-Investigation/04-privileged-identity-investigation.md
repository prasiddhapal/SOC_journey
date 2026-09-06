# 04 | Privileged Identity Investigation

A privileged service account can have significant blast radius if compromised.

Example:

svc_backup
 ├─ SPN
 ├─ weak/old password
 └─ excessive privilege

Potential impact:

TGS request
→ offline cracking
→ credential recovery
→ inherited privileges
→ lateral movement / administrative access

Relevant telemetry:
4624, 4672, 4688, 4768, 4769, 4648, 4728, 4732.
