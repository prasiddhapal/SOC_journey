# Day 28 - Findings

## Summary

Day 28 focused on improving PowerShell detection by adding **execution context, risk scoring, and explainable severity**.

The detection was extended beyond command-line indicators to evaluate the parent process.

## Finding 1: Normal PowerShell Baseline

Observed activity:

```text id="7x3m9q"
explorer.exe
    ↓
powershell.exe -NoProfile
```

Result:

```text id="2k6v4p"
suspicious    = 0
parent_risk   = 0
benign_parent = 1
risk_score    = 0
severity      = Low
```

This established the benign baseline for validation.

## Finding 2: Suspicious PowerShell Behavior

The detection checks for indicators including:

```text id="5q8m1v"
EncodedCommand
-enc
ExecutionPolicy
Download
IEX
```

Test command:

```text id="9v4k2x"
powershell.exe -EncodedCommand ABC123
```

The command was classified as suspicious.

## Finding 3: Parent-Process Context

The suspicious test used:

```text id="3m7q5z"
winword.exe
    ↓
powershell.exe
```

The Office parent process was classified as higher risk:

```text id="6x2p8n"
parent_risk = 1
```

This adds contextual weight to the detection.

## Finding 4: Risk Scoring

The detection combines suspicious behavior and parent-process risk:

```text id="4v9m1k"
risk_score =
    (suspicious * 2)
    +
    (parent_risk * 3)
```

For the suspicious test:

```text id="8q5x2m"
suspicious  = 1
parent_risk = 1
risk_score  = 5
severity    = High
```

## Finding 5: Benign Activity Suppression

Normal PowerShell launched by `explorer.exe` was not escalated.

Result:

```text id="1m6v8q"
risk_score = 0
severity   = Low
```

This demonstrates how execution context can reduce unnecessary escalation.

## Finding 6: Explainable Detection

The detection provides additional triage context through fields such as:

```text id="7p3k9x"
behavior
parent_context
risk_score
severity
reason
```

The suspicious test produced:

```text id="5v8m2q"
Suspicious PowerShell launched by Office application
```

This gives analysts a clear reason for the alert during triage.

## Validation Results

| Scenario                     | Score | Severity |
| ---------------------------- | ----: | -------- |
| Explorer + normal PowerShell |     0 | Low      |
| Word + encoded PowerShell    |     5 | High     |

Both positive and negative test cases produced the expected results.

## Conclusion

Day 28 successfully extended PowerShell detection into a **context-aware detection model**.

The final approach combines:

```text id="9k4x6m"
Behavior
   +
Parent Context
   +
Risk Scoring
   +
Severity
   +
Detection Reason
```

This provides a stronger foundation for detection tuning, alert triage, and SOC investigation.

