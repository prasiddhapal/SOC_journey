# Day 30 Findings

## Finding 1 - Suspicious PowerShell Indicator
The command:

`powershell.exe -EncodedCommand ABC123`

matched the configured suspicious command pattern.

This generated:

`suspicious=1`

## Finding 2 - Process Context
The suspicious PowerShell process was associated with:

`explorer.exe`

The lab detection logic treats Office or common application parents as higher-risk context in earlier modules, but this Day 30 correlation test focuses on event relationships.

## Finding 3 - Follow-On Command
A later event showed:

`powershell.exe -> cmd.exe -> cmd.exe /c whoami`

This provided additional process-chain context.

## Finding 4 - Same Identity and Source
Both events used:

- User: `Administrator`
- Source IP: `10.49.108.48`

The correlation condition therefore identified the events as sharing the same user/source context.

## Finding 5 - Temporal Relationship
The demonstrated events were separated by:

`120 seconds`

This falls inside the five-minute correlation window used by the lab.

## Finding 6 - Correlation Result
The demonstrated two-event scenario produced a correlation score of `2` and the classification:

`Suspicious - Review`

## Analyst Interpretation
The evidence supports investigation and review, but the test data alone should not be treated as proof of compromise.

## Evidence Quality
The strongest evidence in this exercise is the combination of:
1. Suspicious command syntax
2. Related process activity
3. Same identity
4. Same source
5. Short time interval

## Conclusion
The module demonstrates how correlation converts individual telemetry records into a more useful investigation context.
