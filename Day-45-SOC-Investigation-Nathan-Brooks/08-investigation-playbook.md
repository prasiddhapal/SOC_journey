# 08 - SOC Investigation Playbook

## SMB File Activity
1. Identify user.
2. Identify source workstation/IP.
3. Identify destination server/share.
4. Identify target file.
5. Determine access type.
6. Build a timestamped sequence of read/write/delete operations.
7. Correlate authentication and authorization changes.
8. Correlate endpoint process telemetry.
9. Validate direct file telemetry.
10. Assign confidence separately to facts, hypotheses, and conclusions.

## Analyst Discipline
Use language such as:
- **Confirmed:** directly supported by telemetry.
- **Likely:** supported by multiple correlated indicators.
- **Possible:** plausible but lacking direct evidence.
- **Unconfirmed:** evidence insufficient.

Never write `Notepad created the file` when the logs only show that Notepad existed shortly beforehand.
