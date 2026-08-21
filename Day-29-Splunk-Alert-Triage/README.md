# Day 29 — Splunk Context-Aware Detection
## Overview
Day 29 improved PowerShell detection with context, risk scoring, tuning, and analyst decision logic.
```text
Detection → Context → Risk → Decision
```
## Objectives
- Detect suspicious PowerShell commands.
- Evaluate parent-process context.
- Calculate risk.
- Classify severity.
- Enrich events.
- Validate benign behavior.
- Validate suspicious behavior.
## Scenario
Benign:
```text
explorer.exe
 ↓
powershell.exe -NoProfile
```
Suspicious:
```text
winword.exe
 ↓
powershell.exe -EncodedCommand ABC123
```
## Detection Signals
```text
encodedcommand
-enc
executionpolicy
download
iex
```
High-risk parents:
```text
winword.exe
excel.exe
outlook.exe
```
## Risk Model
```text
Risk = (Suspicious × 2) + (Parent Risk × 3)
```
Severity:
```text
5+ → High
2+ → Medium
<2 → Low
```
## Benign Result
```text
Suspicious = 0
Parent Risk = 0
Risk Score = 0
Severity = Low
Decision = No Escalation Required
```
## Suspicious Result
```text
Suspicious = 1
Parent Risk = 1
Risk Score = 5
Severity = High
Decision = Investigate
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
## Validation
| Test | Score | Severity | Result |
|---|---:|---|---|
| Benign PowerShell | 0 | Low | PASS |
| Office + suspicious PowerShell | 5 | High | PASS |
## Investigation Flow
```text
Alert → Triage → Command Analysis → Parent Analysis
→ Context Enrichment → Risk Scoring → Validation → Decision
```
## Evidence
```text
Screenshots/
├── 01-powershell-baseline.png
├── 02-suspicious-command-analysis.png
├── 03-parent-process-context.png
├── 04-risk-score-calculation.png
├── 05-benign-context-validation.png
├── 06-suspicious-context-validation.png
└── 07-final-context-aware-detection.png
```
## Key Lesson
PowerShell should not automatically be treated as malicious.
A stronger detection combines:
```text
Behavior + Context + Risk + Validation
```
## SOC Value
The detection helps answer:
```text
What happened?
Why is it suspicious?
How urgently should it be reviewed?
```
## Skills
`Splunk` `SPL` `Detection Engineering`
`Context Enrichment` `Risk Scoring`
`Detection Validation` `SOC Analysis`
## Lab Scope
All activity was performed in an authorized security laboratory.
No unauthorized systems or infrastructure were targeted.
## Status
**🟢 DAY 29 COMPLETE**
