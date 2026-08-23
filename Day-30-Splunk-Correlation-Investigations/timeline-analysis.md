# Timeline Analysis

## Purpose
Timeline analysis establishes the sequence of events and measures the distance between them.

## Event Sequence

```text
11:38:59
explorer.exe
    |
    +--> powershell.exe
         -EncodedCommand ABC123

11:40:59
powershell.exe
    |
    +--> cmd.exe
         /c whoami
```

## Time Calculation
The lab uses:

```spl
| sort _time
| streamstats current=f window=1 last(_time) as previous_time
| eval gap_seconds=_time-previous_time
```

The resulting gap between the two related events is:

`120 seconds`

## Why Timing Matters
A suspicious process followed shortly by another command-line process can provide useful behavioral context.

Timing alone does not prove malicious activity. It becomes useful when combined with:
- Process relationship
- Command content
- User identity
- Source IP
- Other detection indicators

## Investigation Use
The timeline helps answer:
1. What happened first?
2. What happened next?
3. How quickly did the next action occur?
4. Are the events plausibly connected?

## Result
The PowerShell event preceded the `cmd.exe /c whoami` event by two minutes.

## Analyst Takeaway
A timeline turns raw events into a sequence. This makes investigation reasoning easier to explain and reproduce.

## Validation
The final table exposed `_time`, `previous_time`, and `gap_seconds`, allowing the analyst to verify the calculation directly.
