# Day 28 - Splunk Context-Aware Detection

## Overview

Day 28 extended the PowerShell detection from Day 27 by adding **execution context and risk scoring**.

The detection evaluates:

* PowerShell behavior
* Parent process
* Benign context
* Risk score
* Severity
* Detection reason

## Objectives

* Establish a PowerShell baseline
* Detect suspicious PowerShell commands
* Analyze parent-process context
* Build a risk-scoring model
* Reduce benign activity escalation
* Validate positive and negative cases

## Detection Logic

Suspicious PowerShell indicators include:

```text id="4p7x2m"
EncodedCommand
-enc
ExecutionPolicy
Download
IEX
```

A matching event is marked:

```text id="8k3q5v"
suspicious = 1
```

Office applications are treated as higher-risk parent processes:

```text id="6m9v1x"
winword.exe
excel.exe
outlook.exe
```

These produce:

```text id="2q5n8c"
parent_risk = 1
```

## Risk Scoring

The detection calculates:

```text id="7v4m2k"
risk_score =
    (suspicious * 2)
    +
    (parent_risk * 3)
```

Example:

| Condition                  | Score |
| -------------------------- | ----: |
| Suspicious PowerShell only |     2 |
| Office parent only         |     3 |
| Both signals               |     5 |

### Severity

```text id="9x2q6m"
5+  → High
2+  → Medium
<2  → Low
```

## Benign Context

`explorer.exe` is treated as a benign parent for normal PowerShell activity.

When:

```text id="1k7v3p"
benign_parent = 1
suspicious = 0
```

the risk score is reduced to:

```text id="5m8q2x"
risk_score = 0
severity = Low
```

This helps prevent normal PowerShell activity from being unnecessarily escalated.

## Positive Test

```text id="3v6n9k"
winword.exe
    ↓
powershell.exe -EncodedCommand ABC123
```

Observed:

```text id="7q4m1z"
suspicious  = 1
parent_risk = 1
risk_score  = 5
severity    = High
```

**Detection reason:**

```text id="8x5p2c"
Suspicious PowerShell launched by Office application
```

## Negative Test

```text id="2m9v6k"
explorer.exe
    ↓
powershell.exe -NoProfile
```

Observed:

```text id="4q7n1x"
suspicious    = 0
parent_risk   = 0
benign_parent = 1
risk_score    = 0
severity      = Low
```

This confirms that normal PowerShell activity is not unnecessarily escalated.

## Detection Workflow

```text id="6p3v8m"
PowerShell Event
      ↓
Command Analysis
      ↓
Parent Analysis
      ↓
Risk Score
      ↓
Severity
      ↓
Context + Reason
```

## Key Findings

* PowerShell behavior alone is not always sufficient.
* Parent-process context improves detection confidence.
* Benign context helps reduce false positives.
* Risk scoring makes severity more explainable.
* Positive and negative tests validated the detection logic.

## Outcome

Day 28 moved the detection from basic PowerShell matching toward **context-aware detection engineering**.

The final model combines:

```text id="9k5x2q"
Behavior + Context + Risk + Severity
```

This provides a stronger foundation for SOC detection development.

## Evidence

Screenshots are stored in:

```text id="1v6m8p"
Screenshots/
```

Key evidence covers:

* PowerShell baseline
* Parent-process analysis
* Risk scoring
* Benign validation
* Suspicious validation
* Final detection result

