# Day 29 — Risk Scoring

## Purpose

Day 29 uses a simple explainable risk model to prioritize PowerShell activity.

The model combines:

- Suspicious command indicators
- High-risk parent-process context

## Formula

```text
Risk Score =
(Suspicious × 2)
+
(Parent Risk × 3)
```

## Signal Weights

| Signal | Value |
|---|---:|
| Suspicious command | 2 |
| High-risk parent | 3 |

The parent process receives the larger weight because process ancestry provides important execution context.

## Score Examples

### Benign

```text
Suspicious = 0
Parent Risk = 0

0 × 2 + 0 × 3
= 0
```

### Suspicious Command Only

```text
Suspicious = 1
Parent Risk = 0

1 × 2 + 0
= 2
```

### High-Risk Parent Only

```text
Suspicious = 0
Parent Risk = 1

0 + 1 × 3
= 3
```

### Combined Signals

```text
Suspicious = 1
Parent Risk = 1

1 × 2 + 1 × 3
= 5
```

## Severity Mapping

```text
Risk >= 5 → High
Risk >= 2 → Medium
Otherwise → Low
```

## Day 29 Results

| Scenario | Suspicious | Parent Risk | Score | Severity |
|---|---:|---:|---:|---|
| Normal PowerShell | 0 | 0 | 0 | Low |
| Suspicious command | 1 | 0 | 2 | Medium |
| Office parent | 0 | 1 | 3 | Medium |
| Combined signals | 1 | 1 | 5 | High |

## Why Context Matters

A command indicator alone does not provide the complete picture.

The detection therefore evaluates:

```text
Command
   +
Parent
   =
Contextual Risk
```

This helps distinguish routine administration from more concerning execution chains.

## Analyst Use

Risk scoring supports triage by answering:

```text
How much attention does this event deserve?
```

It does not prove malicious intent.

## Decision Logic

```text
High
 ↓
Investigate immediately

Medium
 ↓
Review suspicious activity

Low
 ↓
No escalation unless other evidence exists
```

## Limitations

The scoring model is intentionally simple.

Production implementations should consider additional context such as:

- Host criticality
- User role
- Frequency
- Network activity
- Known-good administrative tools
- Historical behavior

These were outside the scope of this lab module.

## Key Lesson

Risk scoring should be:

- Explainable
- Consistent
- Context-aware
- Easy for analysts to interpret

## Lab Scope

All testing was conducted in an authorized security laboratory.

## Status

**🟢 Risk Scoring Complete**
