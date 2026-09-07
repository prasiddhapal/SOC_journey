# 02 | Baseline Hunting

Splunk stack-counting was used to distinguish normal volume from rare values.

Event 4624 baseline:
- Type 3: 497
- Type 5: 81
- Type 2: 8
- Type 10: 4
- Type 7: 4

Event 4769 service baseline:
- THM-DC$: 19
- krbtgt: 6
- THM-MKT-WS$: 3
- several services: 1-2

Main lesson: high volume is often normal; rare activity deserves contextual investigation.
