# Day 28 - Risk Scoring

## Overview

Day 28 introduced risk scoring to the PowerShell detection developed in previous modules.

The goal was to combine multiple detection signals into a single, explainable risk score.

## Scoring Signals

### 1. Suspicious PowerShell

Suspicious command indicators set:

```text id="6m2q8v"
suspicious = 1
```

Indicators include:

* `EncodedCommand`
* `-enc`
* `ExecutionPolicy`
* `Download`
* `IEX`

### 2. Parent Process Risk

Office applications are treated as higher-risk parent processes:

```text id="4x7p1n"
winword.exe
excel.exe
outlook.exe
```

These set:

```text id="8q3v5m"
parent_risk = 1
```

## Risk Formula

The scoring model is:

```text id="2k9m6x"
risk_score =
    (suspicious * 2)
    +
    (parent_risk * 3)
```

Parent-process context receives more weight than the command indicator alone.

## Score Examples

| Scenario                   | Suspicious | Parent Risk | Score |
| -------------------------- | ---------: | ----------: | ----: |
| Normal PowerShell          |          0 |           0 |     0 |
| Suspicious PowerShell      |          1 |           0 |     2 |
| Office parent              |          0 |           1 |     3 |
| Suspicious + Office parent |          1 |           1 |     5 |

## Benign Context

`explorer.exe` was used as the benign parent for the normal PowerShell test.

When:

```text id="5v8q2m"
benign_parent = 1
suspicious = 0
```

the score was set to:

```text id="9x4m7k"
risk_score = 0
```

This prevents normal baseline activity from being unnecessarily escalated.

## Severity Mapping

```text id="3q6n1v"
risk_score >= 5  → High
risk_score >= 2  → Medium
otherwise        → Low
```

This provides a consistent relationship between detection signals and alert priority.

## Validation

### Negative Test

```text id="7m2x9p"
explorer.exe
    ↓
powershell.exe -NoProfile
```

Result:

```text id="5k8v3q"
suspicious  = 0
parent_risk = 0
risk_score  = 0
severity    = Low
```

### Positive Test

```text id="1q6m4x"
winword.exe
    ↓
powershell.exe -EncodedCommand ABC123
```

Result:

```text id="8v3p7n"
suspicious  = 1
parent_risk = 1
risk_score  = 5
severity    = High
```

## Findings

The scoring model demonstrates that **execution context can increase detection confidence**.

* Suspicious PowerShell alone produces a lower score.
* Office-launched suspicious PowerShell produces the highest score in this model.
* Benign PowerShell activity remains low risk.

## Conclusion

The Day 28 model combines:

```text id="4n7q2m"
Behavior
   +
Parent Context
   ↓
Risk Score
   ↓
Severity
```

This provides a simple and explainable prioritization model for future context-aware detection tuning.

