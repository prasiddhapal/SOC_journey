# Splunk Transaction Analysis

## Purpose

Day 25 focuses on correlating related Splunk events and building event timelines from a **SOC analyst perspective**.

The goal is to identify suspicious sequences, add context, and validate findings with additional evidence.

## 1. `eventstats`

Calculates statistics while keeping the original events.

```spl
index=main
| eventstats count by user event_id
| table _time user event_id count
```

Useful for identifying repeated activity.

## 2. `streamstats`

Adds sequential context to events.

```spl
index=main
| sort _time
| streamstats count as event_number
| table _time user event_id event_number
```

Useful for building an event timeline.

### Previous Event

```spl
index=main
| sort _time
| streamstats current=f last(event_id) as previous_event
| table _time user event_id previous_event
```

Helps identify what happened immediately before the current event.

### Time Difference

```spl
index=main
| sort _time
| streamstats current=f last(_time) as previous_time
| eval time_diff=_time-previous_time
| table _time user event_id previous_time time_diff
```

Useful for identifying events occurring within a suspicious time window.

## 3. Suspicious Event Sequence

Example: Event ID `4688` follows `4624` within 120 seconds.

```spl
index=main
| sort _time
| streamstats current=f last(event_id) as previous_event
| streamstats current=f last(_time) as previous_time
| eval time_diff=_time-previous_time
| eval suspicious=if(event_id=4688 AND previous_event=4624 AND time_diff<=120,1,0)
| where suspicious=1
| table _time user event_id previous_event time_diff suspicious
```

**SOC note:** A match is an **investigation lead**, not proof of malicious activity. Validate it with additional logs and context.

## 4. `transaction`

Groups related events into a logical transaction.

```spl
index=main
| transaction user
| table user eventcount duration
```

### Transaction Boundaries

```spl
index=main
| transaction user startswith=4624 endswith=4688
| table user eventcount duration event_id process command
```

* `startswith` → defines the starting event
* `endswith` → defines the ending event
* `maxspan` → maximum transaction duration
* `maxpause` → maximum gap between events
* `keepevicted=true` → keeps incomplete transactions

Example:

```spl
index=main
| transaction user maxspan=90s maxpause=30s keepevicted=true
| table user eventcount duration closed_txn
```

## Key Fields

| Field        | SOC Meaning                       |
| ------------ | --------------------------------- |
| `eventcount` | Events in the transaction         |
| `duration`   | Transaction duration              |
| `closed_txn` | Whether the transaction completed |
| `event_id`   | Windows event identifier          |
| `process`    | Process involved                  |
| `command`    | Command executed                  |

## SOC Perspective

Use transaction analysis to turn individual logs into **activity timelines**.

Correlate:

**User → Event ID → Time → Process → Command → Sequence → Duration**

The key question is not just **"What happened?"**

It is:

> **"What happened before and after this event, and does the complete sequence make sense?"**

**Detection is not proof. Correlate, validate, and investigate.**

