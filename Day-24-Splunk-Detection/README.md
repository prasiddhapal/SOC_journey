# Day 24 - Splunk Detection Engineering

## Objective

Build foundational Splunk detection skills by working with security
telemetry and developing basic correlation logic.

## Practical Work

- Splunk SPL filtering and field selection
- `where` for event filtering
- `eval`, `if()`, and `case()` for detection logic
- `stats` for event aggregation
- `dc()` and `values()` for field analysis
- `sort`, `head`, and `tail` for result control
- `rename` and `fields` for result management
- `dedup` for duplicate handling
- Basic `streamstats` event correlation

## Detection Scenario

The investigation used Windows-style authentication and process telemetry.

```text
4624 Successful Logon
        ↓
Administrator
        ↓
10.49.108.37
        ↓
4688 powershell.exe
        ↓
4688 cmd.exe /c whoami
```

## Detection Logic

The practical exercise focused on identifying process creation that
occurred shortly after a successful network logon.

The detection considered:

- Event ID
- User
- Source IP
- Process
- Parent process
- Command line
- Event sequence
- Time difference

## Investigation Result

The observed sequence was classified as:

**Suspicious activity requiring further investigation.**

The available telemetry alone was not sufficient to conclusively
classify the activity as malicious.

Additional investigation would require validation of the source IP,
account usage, and surrounding endpoint or network telemetry.

## Key Lesson

Detection identifies behavior that requires investigation.

A detection should not automatically be treated as proof of malicious
activity. Evidence must be correlated and validated before reaching a
final verdict.

## Status

**Completed** ✅
