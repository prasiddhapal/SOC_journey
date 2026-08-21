# 🚨 SOC Case — [Case Title]

> **Case ID:** `[DAY-XX-CATEGORY]`
> **Case Type:** `[Phishing / Network / Authentication / SIEM / Detection Engineering / Threat Hunting / etc.]`
> **Severity:** `[🔵 Low / 🟡 Medium / 🟠 High / 🔴 Critical]`
> **Status:** `[🟡 Investigating / 🟢 Investigation Complete / 🔴 Escalated]`
> **Environment:** Authorized Security Lab

---

## 🎯 Executive Summary

[Provide a concise summary of the security event, what was investigated, the main finding, and the final assessment.]

**Investigation objective:**
[One sentence describing the primary purpose of the investigation.]

---

## 🧩 Investigation Scenario

[Describe the simulated security event or investigation scenario.]

### Investigation Objectives

* [Objective 1]
* [Objective 2]
* [Objective 3]
* [Objective 4]

---

## 🔎 Key Findings

| Finding     | Result                                    |
| ----------- | ----------------------------------------- |
| [Finding 1] | `[Confirmed / Suspected / Not Confirmed]` |
| [Finding 2] | `[Confirmed / Suspected / Not Confirmed]` |
| [Finding 3] | `[Confirmed / Suspected / Not Confirmed]` |
| [Finding 4] | `[Confirmed / Suspected / Not Confirmed]` |

> **Analyst note:** Distinguish observed evidence from assumptions and unconfirmed conclusions.

---

## 🧬 Indicators of Interest

| Type    | Value          | Relevance          |
| ------- | -------------- | ------------------ |
| IP      | `[IP address]` | `[Why it matters]` |
| Domain  | `[Domain]`     | `[Why it matters]` |
| URL     | `[URL]`        | `[Why it matters]` |
| Hash    | `[Hash]`       | `[Why it matters]` |
| User    | `[Username]`   | `[Why it matters]` |
| Process | `[Process]`    | `[Why it matters]` |

> ⚠️ All indicators in this case are from an authorized lab environment unless explicitly stated otherwise.

---

## 🎯 MITRE ATT&CK Mapping

| Tactic     | Technique     | ID        | Relevance          |
| ---------- | ------------- | --------- | ------------------ |
| `[Tactic]` | `[Technique]` | `[T####]` | `[Why it applies]` |
| `[Tactic]` | `[Technique]` | `[T####]` | `[Why it applies]` |

> Only map techniques supported by the investigation evidence.

---

## 🛰️ Investigation Flow

```text
Alert / Event
     ↓
Initial Triage
     ↓
Evidence Collection
     ↓
Event / Log Analysis
     ↓
IOC Extraction
     ↓
Correlation
     ↓
Detection / Validation
     ↓
Analyst Assessment
     ↓
Response Recommendation
     ↓
Documentation
```

---

## 🧪 Detection Logic

### Detection Objective

[Describe what the detection is intended to identify.]

### Detection Signals

* `[Signal / Indicator 1]`
* `[Signal / Indicator 2]`
* `[Signal / Indicator 3]`

### Contextual Signals

* `[Parent process / user / host / network / authentication context]`
* `[Additional contextual signal]`

### Detection Query / Logic

```text
[Insert SIEM query, detection logic, rule logic, or pseudocode]
```

### Risk / Severity Logic

```text
[Explain how severity or risk is determined.]
```

---

## 🧪 Validation Results

### Negative Test

```text
[Benign scenario / expected normal behavior]
```

**Expected Result:** `[Expected behavior]`

**Observed Result:** `[Observed behavior]`

**Result:** `PASS / FAIL`

---

### Positive Test

```text
[Controlled suspicious scenario]
```

**Expected Result:** `[Expected detection]`

**Observed Result:** `[Observed detection]`

**Result:** `PASS / FAIL`

---

### Validation Summary

| Test          | Expected     | Observed     | Result        |
| ------------- | ------------ | ------------ | ------------- |
| Negative Test | `[Expected]` | `[Observed]` | `PASS / FAIL` |
| Positive Test | `[Expected]` | `[Observed]` | `PASS / FAIL` |

---

## 🛡️ SOC Actions

| Action     | Purpose     | Result     |
| ---------- | ----------- | ---------- |
| `[Action]` | `[Purpose]` | `[Result]` |
| `[Action]` | `[Purpose]` | `[Result]` |
| `[Action]` | `[Purpose]` | `[Result]` |
| `[Action]` | `[Purpose]` | `[Result]` |

### Analyst Workflow

```text
01 — Triage
02 — Investigate
03 — Correlate
04 — Validate
05 — Assess
06 — Respond
07 — Document
```

---

## 🧠 Analyst Assessment

### Confirmed

* [Confirmed finding]
* [Confirmed finding]
* [Confirmed finding]

### Suspected

* [Suspicious activity requiring further investigation]
* [Potential indicator or behavior]

### Not Confirmed

* [Compromise/activity that could not be established]
* [Other unverified conclusion]

> **Analyst Principle:** [State the key analytical principle demonstrated by this case.]

---

## 📋 Recommended Response

For a production alert matching this behavior:

1. [Response action]
2. [Response action]
3. [Response action]
4. [Response action]
5. [Escalation condition, if applicable]

### Escalation Criteria

Escalate when:

* [Condition 1]
* [Condition 2]
* [Condition 3]

---

## 📚 Investigation Evidence

### 🔎 Evidence 01 — [Evidence Description]

[Briefly explain what this evidence shows and why it matters.]

![Evidence 01](Screenshots/01-evidence.png)

---

### 🔎 Evidence 02 — [Evidence Description]

[Briefly explain what this evidence shows and why it matters.]

![Evidence 02](Screenshots/02-evidence.png)

---

### 🔎 Evidence 03 — [Evidence Description]

[Briefly explain what this evidence shows and why it matters.]

![Evidence 03](Screenshots/03-evidence.png)

---

### 🧭 Evidence Chain

```text
Initial Event
     ↓
Evidence 01
     ↓
Evidence 02
     ↓
Evidence 03
     ↓
Correlation
     ↓
Analyst Assessment
     ↓
Response Decision
```

---

## 📊 Investigation Timeline

| Time / Stage | Event     | Analyst Action | Finding     |
| ------------ | --------- | -------------- | ----------- |
| `[Time]`     | `[Event]` | `[Action]`     | `[Finding]` |
| `[Time]`     | `[Event]` | `[Action]`     | `[Finding]` |
| `[Time]`     | `[Event]` | `[Action]`     | `[Finding]` |

---

## 💡 Key Lesson

> [Describe the most important technical or analytical lesson from this investigation.]

### What Improved

**Before:** `[Previous/basic approach]`

**After:** `[Improved investigation/detection approach]`

---

## 📈 Skills Demonstrated

`[SOC Operations]` `[Log Analysis]` `[Threat Hunting]` `[Detection Engineering]` `[Incident Response]`

`[Linux]` `[Windows]` `[Splunk]` `[Network Analysis]` `[Python]`

---

## 🔐 Ethics & Lab Scope

This investigation was conducted in an authorized security laboratory environment for educational and defensive security purposes.

No unauthorized systems, accounts, infrastructure, or data were targeted.

---

## ✅ Case Status

**[🟢 INVESTIGATION COMPLETE / 🟡 IN PROGRESS / 🔴 ESCALATED]**

`[Case ID]` · `[Category]` · `[Technique]` · `[Environment]`
