# Correlation Analysis

## Purpose
This module demonstrates how to correlate related process activity rather than treating each event as an isolated alert.

## Lab Events

### Event 1
- User: `Administrator`
- Source IP: `10.49.108.48`
- Parent: `explorer.exe`
- Process: `powershell.exe`
- PID: `5555`
- Command: `powershell.exe -EncodedCommand ABC123`

### Event 2
- User: `Administrator`
- Source IP: `10.49.108.48`
- Parent: `powershell.exe`
- Process: `cmd.exe`
- PID: `5600`
- Command: `cmd.exe /c whoami`

## Correlation Factors
The investigation compares:
- Same user
- Same source IP
- Suspicious command indicator
- Temporal proximity

## SPL Approach
The lab creates multiple events with `makeresults` and combines them using `append`.

The events are ordered with:

```spl
| sort _time
```

Suspicious command detection uses:

```spl
| eval suspicious=if(match(lower(command),
"encodedcommand|enc|executionpolicy|download|iex"),1,0)
```

## Correlation Concept
A single suspicious PowerShell event provides one indicator.
A related follow-on process provides additional context.

The combined evidence is more useful to an analyst than either event alone.

## Outcome
The correlated events produced a score of `2` and were classified as:

`Suspicious - Review`

## Analyst Lesson
Correlation should increase confidence only when independent evidence supports the relationship. Avoid treating every nearby event as automatically related.
