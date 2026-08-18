# Splunk Transaction Notes

## `eventstats`

Calculates statistics while keeping the original events.

```spl
index=main
| eventstats count by user event_id
```

Useful for identifying repeated activity.

## `streamstats`

Analyzes events in sequence.

```spl
index=main
| sort _time
| streamstats current=f last(event_id) as previous_event
```

Useful for identifying the previous event.

## Time Difference

Calculates the time between events.

```spl
| streamstats current=f last(_time) as previous_time
| eval time_diff=_time-previous_time
```

`time_diff` shows the time between events in seconds.

## `transaction`

Groups related events into one logical transaction.

```spl
| transaction user
| table user eventcount duration
```

## Transaction Controls

| Option        | Purpose                      |
| ------------- | ---------------------------- |
| `startswith`  | Transaction start            |
| `endswith`    | Transaction end              |
| `maxspan`     | Maximum duration             |
| `maxpause`    | Maximum event gap            |
| `keepevicted` | Keep incomplete transactions |

## Important Fields

| Field            | Meaning              |
| ---------------- | -------------------- |
| `eventcount`     | Number of events     |
| `duration`       | Transaction duration |
| `closed_txn`     | Transaction status   |
| `previous_event` | Previous event       |
| `time_diff`      | Time between events  |

## Example Sequence

```text
4624
  ↓
4688
  ↓
4688
```

This can help an analyst understand the sequence of activity around a user or session.

## SOC Lesson

Correlate **user, time, event ID, process, command, and event sequence** before deciding whether activity is suspicious.

**Detection is not proof. Correlate first, then investigate.**

