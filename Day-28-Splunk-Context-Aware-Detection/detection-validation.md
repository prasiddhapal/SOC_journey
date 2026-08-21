# Day 28 - Detection Validation

## Objective

Validate the context-aware PowerShell detection using benign and suspicious test cases.

The goal was to confirm that normal activity remains low-risk while suspicious activity is elevated.

## Validation Model

```text
Detection
   ↓
Behavior Analysis
   ↓
Parent Context
   ↓
Risk Score
   ↓
Severity
```

## Test 1: Benign PowerShell

```text
explorer.exe
    ↓
powershell.exe -NoProfile
```

| Field           | Result |
| --------------- | -----: |
| `suspicious`    |      0 |
| `parent_risk`   |      0 |
| `benign_parent` |      1 |
| `risk_score`    |      0 |
| `severity`      |    Low |

**Result: PASS**

Normal PowerShell activity remained low-risk and was not unnecessarily escalated.

## Test 2: Suspicious PowerShell

```text
winword.exe
    ↓
powershell.exe -EncodedCommand ABC123
```

| Field           | Result |
| --------------- | -----: |
| `suspicious`    |      1 |
| `parent_risk`   |      1 |
| `benign_parent` |      0 |
| `risk_score`    |      5 |
| `severity`      |   High |

**Result: PASS**

The suspicious command combined with an Office parent produced the expected high-risk result.

## Validation Matrix

| Test Case                          | Suspicious | Parent Risk | Score | Severity |
| ---------------------------------- | ---------: | ----------: | ----: | -------- |
| Normal PowerShell                  |          0 |           0 |     0 | Low      |
| Encoded PowerShell + Office parent |          1 |           1 |     5 | High     |

## Analyst Context

The final detection output included:

```text
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

These fields provide useful context for alert triage and investigation.

## Final Result

```text
Benign Test     → PASS
Suspicious Test → PASS
```

The detection successfully kept the benign test at **Low / 0** while the controlled suspicious test reached **High / 5**.

**Final Status: LAB VALIDATED**

