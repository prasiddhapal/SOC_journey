# Day 50 Detection Logic

Authentication Failure -> Success -> Domain Admins Modification

Thresholds:
- 3+ failed authentications
- 1+ successful authentication
- 1+ Domain Admins membership modification
- observed span <= 20 minutes

Severity: HIGH

Analyst action:
Validate authorization, account ownership, source host, recent credential activity, group membership history, and subsequent privileged actions. Do not declare compromise from this detection alone.
