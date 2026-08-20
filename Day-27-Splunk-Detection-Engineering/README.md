# Day 27 - Splunk Detection Engineering

## Overview

Day 27 focused on moving from manual Splunk investigation into reusable detection engineering and validation.

The session used Windows authentication (`4624`) and process creation (`4688`) events to build a time-based correlation and then added suspicious PowerShell command-line detection.

## Learning Objectives

- Correlate authentication with process creation
- Calculate time between related events
- Use `streamstats` for event correlation
- Identify suspicious PowerShell command indicators
- Build analyst-friendly detection output
- Validate both positive and negative detection cases
- Understand why detection logic should be tested before deployment

## Detection Flow

```text
Authentication
      |
      v
Remember authentication time
      |
      v
Process Creation
      |
      v
Within 300 seconds?
      |
      v
Inspect command
      |
      v
Suspicious PowerShell indicator?
      |
      v
Detection
```

## Core Windows Events

| Event ID | Meaning in Lab |
|---|---|
| `4624` | Successful authentication |
| `4688` | Process creation |

## Core Detection Logic

The correlation uses the most recent authentication for the user and calculates the time difference before evaluating the process event.

```spl
index=main (event_id=4624 OR event_id=4688)
| sort _time
| eval auth_time_marker=if(event_id=4624,_time,null())
| eval auth_ip_marker=if(event_id=4624,src_ip,null())
| streamstats current=f last(auth_time_marker) as auth_time last(auth_ip_marker) as auth_src_ip by user
| eval time_since_auth=_time-auth_time
| where event_id=4688 AND time_since_auth <= 300
```

## Suspicious PowerShell Indicators

The lab detection tested these command-line indicators:

```text
encodedcommand
-enc
executionpolicy
download
iex
```

The command is normalized with `lower()` before matching.

```spl
| eval suspicious=if(
    match(lower(command),"encodedcommand|-enc|executionpolicy|download|iex"),
    1,
    0
)
| where suspicious=1
```

## Detection Metadata

The detection produces:

```text
Detection: Suspicious PowerShell After Authentication
Severity: High
```

Analyst-facing fields include:

```text
_time
detection
severity
user
auth_src_ip
time_since_auth
parent
process
pid
command
```

## Validation

### Negative Test

Normal PowerShell:

```text
powershell.exe -NoProfile
```

Result:

```text
No detection
```

A suspicious PowerShell event without recent authentication also produced no detection because it was outside the five-minute correlation window.

### Positive Test

Controlled test:

```text
Authentication: 4624
Process Creation: 4688
Time difference: 60 seconds
User: Administrator
Source IP: 10.49.108.48
Parent: winword.exe
Process: powershell.exe
Command: powershell.exe -EncodedCommand ABC123
```

Result:

```text
Suspicious PowerShell After Authentication
Severity: High
```

## Validation Matrix

| Test Case | Expected | Result |
|---|---|---|
| `powershell.exe -NoProfile` | No detection | No detection |
| Suspicious PowerShell without recent authentication | No detection | No detection |
| Suspicious PowerShell 60 seconds after authentication | Detection | High detection |

## Documentation

- [Detection Engineering](detection-engineering.md)
- [Detection Validation](detection-validation.md)
- [Findings](findings.md)

## Screenshots

The `Screenshots/` directory contains the evidence captured during the Day 27 lab.

```text
01-authentication-process-correlation.png
02-detection-engineering-baseline.png
03-suspicious-powershell-detection.png
04-negative-detection-test.png
05-positive-test-data.png
06-positive-detection-result.png
```

## Key SPL Concepts

| SPL | Purpose |
|---|---|
| `sort _time` | Orders events chronologically |
| `eval` | Creates fields and calculations |
| `streamstats` | Carries previous event information forward |
| `match()` | Searches command-line text |
| `where` | Applies detection conditions |
| `table` | Produces focused analyst output |

## Key Learning

The detection should not be memorized as one large query.

The reusable reasoning pattern is:

```text
Filter
  ->
Create fields
  ->
Correlate events
  ->
Calculate time difference
  ->
Apply conditions
  ->
Match suspicious behavior
  ->
Produce analyst output
  ->
Validate
```

## Current Day 27 Status

Completed:

- Detection Engineering
- Detection Validation
- Negative testing
- Positive testing
- Findings documentation

Deferred to the next session:

- False-positive tuning
- Full alert investigation workflow
- Final production-oriented detection tuning

## Repository Structure

```text
Day-27-Splunk-Detection-Engineering/
|
|-- detection-engineering.md
|-- detection-validation.md
|-- findings.md
|-- README.md
|
`-- Screenshots/
    |-- 01-authentication-process-correlation.png
    |-- 02-detection-engineering-baseline.png
    |-- 03-suspicious-powershell-detection.png
    |-- 04-negative-detection-test.png
    |-- 05-positive-test-data.png
    `-- 06-positive-detection-result.png
```

## Note

This documentation reflects the controlled Day 27 lab work. The detection was validated against the available lab and synthetic test data and should not be treated as production-ready without additional tuning and validation.
