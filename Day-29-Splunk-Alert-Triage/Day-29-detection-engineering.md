# Day 29 — Detection Engineering
## Overview
Day 29 builds a context-aware PowerShell detection in Splunk.
The detection combines command indicators, parent context, risk scoring, severity, tuning, and analyst decisions.
## Objective
Identify PowerShell activity that becomes more suspicious when suspicious command indicators and a high-risk parent process occur together.
## Detection Flow
```text
PowerShell → Command → Parent Context → Risk → Severity → Decision
```
## Event Fields
| Field | Purpose |
|---|---|
| `_time` | Timestamp |
| `user` | Account |
| `src_ip` | Source |
| `parent` | Parent process |
| `process` | Child process |
| `pid` | Process ID |
| `command` | Command line |
## Command Indicators
```text
encodedcommand
-enc
executionpolicy
download
iex
```
A match produces `suspicious=1`; otherwise `suspicious=0`.
## Parent Context
High-risk parents tested:
```text
winword.exe
excel.exe
outlook.exe
```
A match produces `parent_risk=1`; otherwise `parent_risk=0`.
## Risk Formula
```text
risk_score =
(suspicious × 2) +
(parent_risk × 3)
```
Combined suspicious case:
```text
1 × 2 + 1 × 3 = 5
```
## Severity
```text
5+ → High
2+ → Medium
<2 → Low
```
## Context Fields
```text
behavior
parent_context
reason
tuning
analyst_decision
analyst_summary
```
## Benign Scenario
```text
explorer.exe
 ↓
powershell.exe -NoProfile
```
Expected: `suspicious=0`, `parent_risk=0`, `risk_score=0`, `severity=Low`.
## Suspicious Scenario
```text
winword.exe
 ↓
powershell.exe -EncodedCommand ABC123
```
Expected: `suspicious=1`, `parent_risk=1`, `risk_score=5`, `severity=High`.
## Detection Philosophy
PowerShell alone is not automatically malicious.
```text
Behavior + Context + Risk = Decision
```
## Analyst Workflow
```text
Detect → Analyze → Enrich → Score → Classify → Validate → Decide
```
## Validation
Day 29 completed negative benign validation and positive suspicious validation. Both produced expected results.
## Analyst Output
The final event contains indicators, parent context, risk, severity, reason, tuning, decision, and summary.
## Key Takeaway
The project moved from simple PowerShell matching to contextual detection.
## Lab Scope
All activity was performed in an authorized security laboratory.
## Status
**🟢 Detection Engineering Complete**
