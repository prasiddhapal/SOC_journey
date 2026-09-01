# 04 - Windows Event Investigation

## Process Execution Search

```spl
index=task4 EventCode=1 Image="*SharePoint.exe"
| table _time ComputerName User Image CommandLine Hashes
```

## Purpose

This search focuses on process-creation telemetry involving an image matching `SharePoint.exe`.

## Useful Fields

- `_time`
- `ComputerName`
- `User`
- `Image`
- `CommandLine`
- `Hashes`

## Why These Fields Matter

The image identifies the process.

The command line provides execution context.

The user identifies the associated account.

The computer identifies the affected endpoint.

Hashes can support later file identification or comparison.

## Network Event Search

A Windows network-event investigation can use fields such as:

- SourceIp
- SourcePort
- DestinationIp
- DestinationPort
- Protocol

## Correlation

Process execution should be correlated with network activity.

For example:

1. Process starts.
2. Process makes a network connection.
3. Connection reaches an unusual destination.
4. Additional host activity follows.

The sequence provides more context than any single event.

## Analyst Principle

Start with the event.

Extract fields.

Correlate.

Then conclude.
