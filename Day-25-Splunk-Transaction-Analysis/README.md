# Day 25 - Splunk Transaction Analysis

## Overview

Day 25 focuses on Splunk event correlation and transaction analysis.

## Objectives

* Understand event correlation
* Use `eventstats`
* Use `streamstats`
* Analyze event sequences
* Calculate time differences
* Use `transaction`
* Understand transaction boundaries

## Event Statistics

`eventstats` calculates statistics while keeping the original events.

```spl
index=main
| eventstats count by user event_id
| table _time user event_id count
```

## Sequential Analysis

`streamstats` performs calculations across events in sequence.

```spl
index=main
| sort _time
| streamstats current=f last(event_id) as previous_event
| table _time user event_id previous_event
```

## Time Analysis

The previous timestamp can be used to calculate the time between events.

```spl
index=main
| sort _time
| streamstats current=f last(_time) as previous_time
| eval time_diff=_time-previous_time
| table _time user event_id previous_time time_diff
```

## Transaction Analysis

Transactions group related events into a logical activity.

```spl
index=main
| transaction user
| table user eventcount duration
```

## Transaction Boundaries

Transaction boundaries can be defined using `startswith` and `endswith`.

```spl
index=main
| transaction user startswith=4624 endswith=4688
| table user eventcount duration
```

## Transaction Controls

* `maxspan` - Maximum transaction duration
* `maxpause` - Maximum gap between events
* `keepevicted` - Keeps incomplete transactions
* `closed_txn` - Indicates transaction completion status

## Investigation Flow

```text
Events
  ↓
Sort by time
  ↓
Analyze sequence
  ↓
Calculate time difference
  ↓
Correlate events
  ↓
Build transaction
  ↓
Validate evidence
```

## Key Takeaway

Transaction analysis helps a SOC analyst understand related events as a sequence instead of treating every log entry independently.

> Detection is not proof. Correlate evidence first.

## Documentation Structure

The **Event Statistics**, **Sequential Analysis**, and **Time Analysis** sections belong in this same `README.md`.

