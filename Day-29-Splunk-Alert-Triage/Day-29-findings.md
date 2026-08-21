# Day 29 — Findings
## Executive Summary
Day 29 demonstrated a context-aware PowerShell detection in Splunk.
The detection distinguishes normal PowerShell from suspicious PowerShell launched by a high-risk Office parent.
## Finding 01 — Command Detection
**Status:** Confirmed
Indicators include:
```text
encodedcommand
-enc
executionpolicy
download
iex
```
A match produces `suspicious=1`.
## Finding 02 — Parent Context
**Status:** Confirmed
High-risk parents include:
```text
winword.exe
excel.exe
outlook.exe
```
A match produces `parent_risk=1`.
## Finding 03 — Risk Calculation
**Status:** Confirmed
```text
(suspicious × 2) + (parent_risk × 3)
```
The combined suspicious test produced `risk_score=5` and `severity=High`.
## Finding 04 — Benign Validation
**Status:** Confirmed
```text
explorer.exe
 ↓
powershell.exe -NoProfile
```
Result:
```text
risk_score=0
severity=Low
decision=No Escalation Required
```
## Finding 05 — Suspicious Validation
**Status:** Confirmed
```text
winword.exe
 ↓
powershell.exe -EncodedCommand ABC123
```
Result:
```text
suspicious=1
parent_risk=1
risk_score=5
severity=High
```
Decision:
```text
Investigate - High Confidence Suspicious Activity
```
## Finding 06 — Context Improves Triage
**Status:** Confirmed
The detection provides behavior, parent context, reason, tuning, analyst decision, and analyst summary.
## Not Confirmed
The lab evidence does not establish actual compromise, persistence, credential theft, data exfiltration, or successful malicious execution.
## Analyst Assessment
Suspicious PowerShell combined with a high-risk Office parent warrants investigation but does not independently prove compromise.
## Key Lesson
```text
Indicator + Context + Risk = Better SOC Decision
```
## Evidence
Supporting screenshots are stored in:
```text
Screenshots/
```
## Lab Scope
All findings come from controlled, authorized lab testing.
## Status
**🟢 Investigation Complete**
