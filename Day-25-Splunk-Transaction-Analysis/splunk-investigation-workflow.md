# Splunk Investigation Workflow

## Objective

Use event correlation and transaction analysis to build investigation context from Splunk logs.

## Workflow

```text
Event
  ↓
Filter
  ↓
Sort by Time
  ↓
Check Previous Event
  ↓
Calculate Time Difference
  ↓
Correlate Events
  ↓
Build Transaction
  ↓
Validate Evidence
  ↓
Conclusion
```

## Investigation Questions

* Who performed the activity?
* What happened first?
* What happened next?
* How much time passed?
* What process was involved?
* What command was executed?
* Are the events related?
* Was the transaction completed?
* Does the activity require investigation?

## Example Sequence

```text
4624
  ↓
4688
  ↓
4688
```

This sequence provides context that can be investigated further.

## Key Principle

A detection is an **investigation lead**, not proof of malicious activity.

**Correlate the surrounding evidence before reaching a conclusion.**

