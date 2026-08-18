# Day 25 - Findings

## Summary

Day 25 focused on **Splunk event correlation, sequence analysis, and transaction analysis**.

## Key Findings

### Event Analysis

`eventstats` calculates event statistics while keeping the original events.

### Sequence Analysis

`streamstats` tracks previous events and timestamps to build event context.

### Time Correlation

Time differences help determine how quickly related events occurred.

### Detection

A sequence such as:

```text id="q5qv8h"
4624 → 4688
```

can be flagged as an **investigation lead** and correlated with additional evidence.

### Transaction Analysis

`transaction` groups related events into a logical activity.

Key controls:

* `startswith` → Defines the beginning
* `endswith` → Defines the ending
* `maxspan` → Limits total duration
* `maxpause` → Limits the gap between events
* `keepevicted` → Preserves incomplete transactions

## Investigation Lesson

Transaction results provide context, but they **do not automatically prove malicious activity**.

## Final Takeaway

**Correlate the user, time, event ID, process, command, and event sequence before reaching a conclusion.**

