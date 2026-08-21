# Day 29 — Detection Validation

## Purpose

This document records validation of the Day 29 context-aware PowerShell detection.

The validation confirms that the detection:

- Recognizes suspicious command indicators.
- Recognizes high-risk parent processes.
- Calculates the expected risk.
- Separates benign and suspicious behavior.
- Produces an analyst decision.

## Validation Model

```text
Input Event
    ↓
Detection Logic
    ↓
Context
    ↓
Risk
    ↓
Severity
    ↓
Decision
```

## Negative Test

### Input

```text
parent  = explorer.exe
process = powershell.exe
command = powershell.exe -NoProfile
```

### Expected

```text
suspicious = 0
parent_risk = 0
risk_score = 0
severity = Low
```

### Observed

```text
behavior       = Normal PowerShell
parent_context = Normal Parent
reason         = No strong suspicious indicators
tuning         = Benign PowerShell
```

### Result

**PASS**

The benign event did not escalate.

## Positive Test

### Input

```text
parent  = winword.exe
process = powershell.exe
command = powershell.exe -EncodedCommand ABC123
```

### Expected

```text
suspicious = 1
parent_risk = 1
risk_score = 5
severity = High
```

### Observed

```text
behavior       = Suspicious PowerShell
parent_context = Office Application Parent
risk_score     = 5
severity       = High
```

### Result

**PASS**

The suspicious event received high-confidence investigation priority.

## Validation Summary

| Test | Risk | Severity | Result |
|---|---:|---|---|
| Benign PowerShell | 0 | Low | PASS |
| Office + suspicious PowerShell | 5 | High | PASS |

## Tuning Validation

The detection correctly produces different tuning outcomes:

```text
Benign PowerShell
        ↓
Benign PowerShell

Suspicious + Office Parent
        ↓
High Confidence - Review Immediately
```

## Analyst Decision

The suspicious event is routed toward investigation rather than automatically treated as confirmed compromise.

This preserves the distinction between:

```text
Detection
    ≠
Confirmed Incident
```

## Evidence

Validation evidence is stored under:

```text
Screenshots/
```

Relevant screenshots cover:

1. PowerShell baseline
2. Suspicious command analysis
3. Parent-process context
4. Risk calculation
5. Benign validation
6. Suspicious validation
7. Final detection

## Key Lesson

A useful detection must demonstrate both:

```text
True Positive Detection
+
Benign Behavior Handling
```

Day 29 passed both controlled validation paths.

## Lab Scope

Testing was performed only in an authorized security laboratory.

## Status

**🟢 Detection Validation Complete**
