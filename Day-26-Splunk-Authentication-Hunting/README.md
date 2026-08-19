# Day 26 - Splunk Authentication Hunting

## Objective

Investigate Windows authentication activity in Splunk and identify suspicious login patterns.

## Topics

* Event IDs `4624`, `4625`, `4672`
* Logon types
* Source IP analysis
* Failed login hunting
* Brute-force detection
* Password spraying
* Authentication correlation
* Detection engineering

## Environment

* Splunk Enterprise
* Index: `main`

## Key Events

| Event ID | Meaning                     |
| -------- | --------------------------- |
| `4624`   | Successful logon            |
| `4625`   | Failed logon                |
| `4672`   | Special privileges assigned |

## Important Fields

```text
_time
user
src_ip
dest_ip
event_id
logon_type
```

## Logon Types

Logon Type describes how the authentication occurred.

| Type | Meaning            |
| ---- | ------------------ |
| `2`  | Interactive        |
| `3`  | Network            |
| `5`  | Service            |
| `10` | Remote Interactive |

## Field Discovery

```spl
index=main event_id=4624
| fieldsummary
```

## Successful Authentication

```spl
index=main event_id=4624
| table _time user src_ip dest_ip event_id logon_type action
| sort _time
```

## Failed Authentication

```spl
index=main event_id=4625
| stats count by user src_ip
| sort - count
```

## Brute-Force Detection

A common pattern is:

**Same user + same source IP + multiple failed logons**

```spl
index=main event_id=4625
| stats count by user src_ip
| where count >= 3
```

The threshold is a hunting example, not proof of brute force.

## Password Spraying

A common pattern is:

**Same source IP + multiple targeted users + failed logons**

```spl
index=main event_id=4625
| stats dc(user) as unique_users count by src_ip
| where unique_users >= 3
```

## Authentication Correlation

Example sequence:

```text
4625
  ↓
4625
  ↓
4625
  ↓
4624
```

Repeated failures followed by a successful login should be investigated with additional context.

## Investigation Questions

* Who authenticated?
* Where did the authentication originate?
* What was the logon type?
* Were there previous failures?
* Was one account targeted?
* Were multiple accounts targeted?
* What happened after authentication?

## Analyst Principle

Do not automatically classify a suspicious pattern as malicious.

```text
Evidence
   ↓
Pattern
   ↓
Context
   ↓
Correlation
   ↓
Risk Assessment
```

## Day 26 Outcome

Completed practical authentication hunting in Splunk, focusing on failed logons, brute-force patterns, password spraying, and authentication correlation.

