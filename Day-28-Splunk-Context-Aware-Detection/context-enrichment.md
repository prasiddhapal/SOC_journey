# Day 28 - Context Enrichment

## Overview

Day 28 extended the PowerShell detection by adding **execution context**.

Instead of evaluating PowerShell only by its command line, the detection also considers the parent process and surrounding context.

## Purpose

Context enrichment helps answer:

* What happened?
* Who launched the process?
* How was it executed?
* How risky is the combination?

Key context fields:

```text id="6m2q8v"
parent
parent_risk
benign_parent
parent_context
```

## Parent Process Analysis

PowerShell activity was analyzed together with its parent process.

### Normal Baseline

```text id="4v7n2x"
explorer.exe
    ↓
powershell.exe
```

### Suspicious Test

```text id="9k3m6q"
winword.exe
    ↓
powershell.exe
```

The parent process provides additional context for interpreting PowerShell activity.

## Risky Parent Context

The detection treats these Office applications as higher-risk PowerShell parents:

```text id="2x8p5m"
winword.exe
excel.exe
outlook.exe
```

When matched:

```text id="7q4v1n9"
parent_risk = 1
```

Otherwise:

```text id="5m2k8x"
parent_risk = 0
```

## Benign Parent Context

The normal test used `explorer.exe` as the benign parent.

When matched:

```text id="8v3q6m"
benign_parent = 1
```

This helps distinguish normal PowerShell activity from higher-risk execution contexts.

## Context Classification

The detection creates a readable context field.

**Office parent:**

```text id="1k7m4x"
parent_context = Office Application Parent
```

**Other parent:**

```text id="6q2v9p"
parent_context = Normal Parent
```

This makes the detection easier for an analyst to interpret.

## Context and Risk

Suspicious PowerShell combined with a higher-risk parent increases the overall risk score.

```text id="3x8m5q"
Suspicious Command
       +
Office Parent
       ↓
Higher Risk
```

The scoring model is:

```text id="9v4k2m"
risk_score =
    (suspicious * 2)
    +
    (parent_risk * 3)
```

## Benign Example

```text id="7m1q8x"
explorer.exe
    ↓
powershell.exe -NoProfile
```

Result:

```text id="5k3v9p"
suspicious    = 0
parent_risk   = 0
benign_parent = 1
risk_score    = 0
severity      = Low
```

## Suspicious Example

```text id="2q6m4v"
winword.exe
    ↓
powershell.exe -EncodedCommand ABC123
```

Result:

```text id="8x5n1k"
suspicious    = 1
parent_risk   = 1
benign_parent = 0
risk_score    = 5
severity      = High
```

## Analyst Context

The final detection can expose:

```text id="4m7q2x"
user
src_ip
parent
process
pid
command
behavior
parent_context
risk_score
severity
reason
```

This gives the analyst both the event and the context needed for triage.

## Key Finding

**PowerShell should not be evaluated in isolation.**

The parent process provides an additional behavioral signal that can increase or decrease detection confidence.

## Conclusion

Day 28 introduced context enrichment by combining:

```text id="6v2m8q"
PowerShell Behavior
       +
Parent Process
       +
Benign Context
       ↓
Risk-Based Detection
```

This moved the detection beyond simple command matching toward a more **contextual, explainable, and SOC-focused detection model**.

