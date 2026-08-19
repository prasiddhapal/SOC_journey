# Authentication Hunting

## Overview

Authentication hunting focuses on identifying and investigating Windows authentication activity in Splunk.

## Investigation Goals

* Who authenticated?
* From where?
* When?
* Was authentication successful?
* What type of logon occurred?
* What happened before or after authentication?

## Windows Authentication Events

| Event ID | Meaning                     |
| -------- | --------------------------- |
| `4624`   | Successful logon            |
| `4625`   | Failed logon                |
| `4672`   | Special privileges assigned |

## Important Fields

```text id="1x4j2n"
_time
user
src_ip
dest_ip
event_id
logon_type
action
```

## Field Discovery

```spl id="5rj4x9"
index=main event_id=4624
| fieldsummary
```

`fieldsummary` helps identify available fields and their values.

## Successful Logon Hunting

```spl id="yq8x1m"
index=main event_id=4624
| table _time user src_ip dest_ip event_id logon_type action
| sort _time
```

**Lab evidence:**

```text id="v4n8qx"
User       : Administrator
Source IP  : 10.49.108.37
Event ID   : 4624
Logon Type : 3
Action     : successful_logon
```

## Logon Type

Logon Type identifies how authentication occurred.

| Type | Meaning            |
| ---- | ------------------ |
| `2`  | Interactive        |
| `3`  | Network            |
| `5`  | Service            |
| `10` | Remote Interactive |

`logon_type=3` means **Network Logon**. It does not mean three login attempts. Humans have suffered enough from confusing numbers with meanings.

## Failed Authentication

```spl id="d6j0jz"
index=main event_id=4625
| stats count by user src_ip
| sort - count
```

No `4625` events were observed in the available lab dataset.

Controlled simulations were used to practice failed-authentication detection.

## Brute-Force Pattern

Typical pattern:

**Same user + same source IP + multiple failed logons**

Example:

```spl id="bq6qwy"
| stats count by user src_ip
| where count >= 3
```

The threshold is a hunting example, not proof of malicious activity.

## Password Spraying

Typical pattern:

**Same source IP + multiple users + failed authentication**

```spl id="7w22zv"
| stats dc(user) as unique_users count by src_ip
| where unique_users >= 3
```

`dc(user)` returns the distinct count of users.

## Failed → Successful Authentication

Example pattern:

```text id="x6qv4w"
4625
  ↓
4625
  ↓
4625
  ↓
4624
```

Investigate:

* Same user
* Same source IP
* Time interval
* Account privileges
* Activity after successful logon

## Authentication Timeline

```spl id="g4e1k8"
index=main
| sort _time
| streamstats current=f last(event_id) as previous_event
| streamstats current=f last(_time) as previous_time
| eval time_diff=_time-previous_time
| table _time user src_ip event_id action previous_event time_diff
```

## Evidence Discipline

Do not turn missing evidence into a conclusion.

```text id="a7qz9m"
No 4625 observed
≠
No failed logons ever occurred

No 4672 observed
≠
No privileged activity occurred
```

Use:

```text id="k8p3lw"
Evidence
   ↓
Pattern
   ↓
Context
   ↓
Correlation
   ↓
Assessment
```

## Day 26 Lab Finding

**Observed authentication:**

```text id="0p2m7c"
4624
Administrator
10.49.108.37
logon_type=3
successful_logon
```

No `4625` or `4672` events were observed in the available dataset.

Controlled simulations covered:

* Failed authentication
* Brute-force detection
* Password spraying
* Failed → successful authentication

## Key Takeaway

Authentication hunting correlates:

**User + Source IP + Event ID + Logon Type + Time + Authentication Pattern + Post-Authentication Activity**

The goal is to turn authentication events into **investigative evidence**, not assumptions.

