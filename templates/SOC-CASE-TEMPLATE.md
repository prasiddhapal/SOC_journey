# 🚨 SOC Case — Context-Aware PowerShell Detection

> **Case ID:** `DAY-28-SPLUNK-CONTEXT`
> **Case Type:** SIEM / Detection Engineering
> **Severity:** 🟠 High
> **Status:** 🟢 Investigation Complete
> **Environment:** Authorized Security Lab

## 🎯 Executive Summary

A context-aware PowerShell detection was developed and validated in Splunk.

The detection combines **PowerShell command behavior** with **parent-process context** to improve risk assessment and reduce unnecessary escalation.

A benign PowerShell execution remained **Low / 0**, while a controlled Office-launched encoded PowerShell execution reached **High / 5**.

## 🧩 Investigation Scenario

The lab contained PowerShell process events with different parent processes and command-line behaviors.

### Objectives

* Establish a PowerShell baseline
* Identify suspicious command indicators
* Enrich events with parent-process context
* Calculate a risk score
* Validate benign and suspicious scenarios
* Produce explainable detection results

## 🔎 Key Findings

| Finding                       | Result    |
| ----------------------------- | --------- |
| Normal PowerShell activity    | Confirmed |
| Suspicious PowerShell command | Confirmed |
| Office parent context         | Confirmed |
| Benign parent context         | Confirmed |
| Risk scoring                  | Validated |
| Positive test                 | PASS      |
| Negative test                 | PASS      |

## 🧬 Indicators of Interest

| Type                 | Value             |
| -------------------- | ----------------- |
| Source IP            | `10.49.108.48`    |
| User                 | `Administrator`   |
| Parent Process       | `winword.exe`     |
| Process              | `powershell.exe`  |
| Suspicious Indicator | `-EncodedCommand` |
| PID                  | `5555`            |

> These are controlled lab values and are not production IOCs.

## 🛰️ Investigation Flow

```text id="8m2q7v"
PowerShell Event
       ↓
Command Analysis
       ↓
Suspicious Indicator
       ↓
Parent Process Context
       ↓
Risk Score
       ↓
Severity
       ↓
Validation
       ↓
Analyst Assessment
```

## 🧮 Detection Logic

Suspicious PowerShell indicators included:

```text id="4v7n1x"
EncodedCommand
-enc
ExecutionPolicy
Download
IEX
```

Higher-risk parent processes included:

```text id="6q3m8p"
winword.exe
excel.exe
outlook.exe
```

### Risk Formula

```text id="9k5x2m"
risk_score =
    (suspicious * 2)
    +
    (parent_risk * 3)
```

This model gives additional weight to parent-process context.

## 🧪 Validation Results

### Negative Test

```text id="2m8q6v"
explorer.exe
    ↓
powershell.exe -NoProfile
```

```text id="7x3p9k"
suspicious    = 0
parent_risk   = 0
risk_score    = 0
severity      = Low
```

**Result: PASS**

### Positive Test

```text id="5v1m8q"
winword.exe
    ↓
powershell.exe -EncodedCommand ABC123
```

```text id="3q7x2n"
suspicious  = 1
parent_risk = 1
risk_score  = 5
severity    = High
```

**Result: PASS**

## 🛡️ SOC Actions

| Action              | Purpose                        |
| ------------------- | ------------------------------ |
| Process baseline    | Establish normal behavior      |
| Command analysis    | Identify suspicious PowerShell |
| Parent enrichment   | Add execution context          |
| Risk scoring        | Prioritize events              |
| Positive validation | Confirm detection behavior     |
| Negative validation | Test false-positive behavior   |

## 🧠 Analyst Assessment

### Confirmed

* PowerShell behavior was evaluated from command data.
* Parent-process context increased detection confidence.
* Office-launched PowerShell received elevated risk.
* Explorer-launched PowerShell remained Low risk.
* The detection produced explainable output.

### Not Confirmed

* Real-world compromise
* External malicious infrastructure
* Production incident
* Credential theft or persistence

> **Analyst Principle:** Evaluate suspicious behavior in context rather than relying on a single indicator.

## 📋 Recommended Response

For a production alert matching this behavior:

1. Review the PowerShell command line.
2. Investigate the parent process.
3. Identify the initiating user.
4. Review related process activity.
5. Correlate authentication and network events.
6. Escalate when additional malicious indicators are present.

## 📚 Investigation Evidence

### 🔎 Evidence 01 — PowerShell Baseline

Normal PowerShell execution was established using `explorer.exe` as the parent process.

### 🔎 Evidence 02 — Suspicious Command

The encoded PowerShell command matched the configured suspicious indicators.

### 🔎 Evidence 03 — Parent Context

`winword.exe` was identified as a higher-risk parent process.

### 🔎 Evidence 04 — Risk Score

The suspicious command combined with the Office parent produced:

```text id="1n6q4v"
risk_score = 5
severity   = High
```

### 🔎 Evidence 05 — Benign Validation

Normal PowerShell activity produced:

```text id="8m2x7q"
risk_score = 0
severity   = Low
```

### 🔎 Evidence 06 — Final Detection

The final detection provided:

**Behavior + Parent Context + Risk Score + Severity + Reason**

## 💡 Key Lesson

Detection engineering becomes stronger when events are evaluated using multiple contextual signals.

Day 28 progressed from simple PowerShell matching toward **context-aware, risk-based, and explainable SOC detection**.

## ✅ Case Status

**INVESTIGATION COMPLETE — LAB VALIDATED**

`DAY-28-SPLUNK-CONTEXT` · `Detection Engineering` · `PowerShell` · `Process Context`

## 📈 SOC Journey

```text id="6v3m9x"
Day 20 ─ SOC Phishing Investigation
   ↓
Day 21 ─ Alert Triage / Network Investigation
   ↓
Day 22 ─ Windows Event Investigation
   ↓
Day 23 ─ Splunk Investigation
   ↓
Day 24 ─ Splunk Detection
   ↓
Day 25 ─ Transaction Analysis
   ↓
Day 26 ─ Authentication Hunting
   ↓
Day 27 ─ PowerShell Detection
   ↓
Day 28 ─ Context-Aware Detection
```

### Current Direction

```text id="2q8m5v"
Investigation
     ↓
Detection
     ↓
Validation
     ↓
Context Enrichment
     ↓
Risk Scoring
     ↓
Explainable SOC Detection
```
