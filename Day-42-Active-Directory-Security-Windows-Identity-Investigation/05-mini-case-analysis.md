# 05 | Mini Case Analysis

## Evidence
4624 + 4672 + 4688 + 4769 all involve svc_backup.

## Observation
The privileged service account was used from a finance workstation that had not previously used it.

## Hypothesis
Possible credential compromise, potentially involving Kerberoasting.

## Confidence
Medium-High.

## Next steps
- isolate the workstation
- reset/rotate svc_backup credentials
- invalidate active sessions/tickets as appropriate
- investigate endpoint artifacts
- hunt for additional svc_backup use
- review whether Domain Admin privilege is justified

## Why this matters
The concern comes from correlation, not from a single event.
