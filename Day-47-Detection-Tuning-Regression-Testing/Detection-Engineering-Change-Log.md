# Detection Engineering Change Log

## Version 1.0 — Day 46 Baseline
**Detection:** Office Application Spawning Encoded PowerShell

Logic:
- Office parent
- PowerShell child
- `-enc` or `-EncodedCommand`

Limitation:
- Did not detect a Word → PowerShell case that used hidden execution plus `Invoke-WebRequest` without `-EncodedCommand`.

## Version 1.1 — Day 46 Tuning
Added:
- `-WindowStyle Hidden`
- `-w hidden`

Explicitly excluded from suspicious criteria:
- `-NoProfile` by itself

Reason:
`-NoProfile` is common in legitimate automation and is weak evidence without supporting behavior.

## Day 47 Regression Requirement
Every future modification must re-run:
- Benign regression cases
- Suspicious regression cases
- Edge cases
- Known detection gaps

No tuning change should be accepted solely because it makes one alert look better.
