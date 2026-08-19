# Day 26 - Detection Queries

## 1. Discover Authentication Fields

```spl
index=main event_id=4624
| fieldsummary
```

**Purpose:** Identify available fields and their values.

## 2. Successful Authentication

```spl
index=main event_id=4624
| table _time user src_ip dest_ip event_id logon_type action
| sort _time
```

**Purpose:**

* Identify successful logons
* Identify the user and source IP
* Identify the logon type
* Build an authentication timeline

## 3. Failed Authentication

```spl
index=main event_id=4625
| stats count by user src_ip
| sort - count
```

**Purpose:** Identify failed authentication activity by user and source IP.

## 4. Brute-Force Detection

```spl
index=main event_id=4625
| stats count by user src_ip
| where count >= 3
```

**Detection logic:**

**Same user + same source IP + 3+ failed logons**

This threshold is a detection lead, not proof of compromise.

## 5. Password Spraying Detection

```spl
index=main event_id=4625
| stats dc(user) as unique_users count by src_ip
| where unique_users >= 3
```

`dc(user)` returns the number of distinct users.

**Detection logic:**

**Same source IP + multiple users + failed authentication**

## 6. Authentication Timeline

```spl
index=main
| sort _time
| streamstats current=f last(event_id) as previous_event
| streamstats current=f last(_time) as previous_time
| eval time_diff=_time-previous_time
| table _time user src_ip event_id action previous_event time_diff
```

**Purpose:**

* Track event order
* Identify previous events
* Calculate time differences
* Correlate authentication activity

## 7. Successful + Failed Authentication

```spl
index=main (event_id=4624 OR event_id=4625)
| sort _time
| table _time user src_ip event_id logon_type action
```

**Purpose:** View successful and failed authentication events together.

## 8. Privileged Authentication Hunt

```spl
index=main event_id=4672
| table _time user event_id
| sort _time
```

**Purpose:** Search for special privilege assignment events.

If no results appear:

> No `4672` events observed in the available dataset.

## 9. Network Logon Hunt

```spl
index=main event_id=4624 logon_type=3
| table _time user src_ip dest_ip event_id logon_type action
| sort _time
```

**Purpose:** Identify successful Network Logon activity.

## 10. Source-to-User Baseline

```spl
index=main event_id=4624
| stats count by user src_ip
| sort - count
```

**Purpose:** Understand normal user-to-source relationships and identify unusual combinations.

## 11. Failed Authentication Alert

```spl
index=main event_id=4625
| stats count by user src_ip
| where count >= 3
| eval alert="Possible Brute Force"
| table user src_ip count alert
```

**Purpose:** Create an analyst-friendly brute-force detection result.

## 12. Password Spray Alert

```spl
index=main event_id=4625
| stats dc(user) as unique_users count by src_ip
| where unique_users >= 3
| eval alert="Possible Password Spraying"
| table src_ip unique_users count alert
```

**Purpose:** Create an analyst-friendly password-spraying detection.

## 13. Authentication Correlation

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

Investigate:

* Same user
* Same source IP
* Time interval
* Successful authentication
* Post-authentication activity

## Detection Principles

```text
Event
  ↓
Filter
  ↓
Group
  ↓
Count
  ↓
Threshold
  ↓
Correlation
  ↓
Investigation
```

**Do not treat a detection as automatic proof of compromise.**

Always validate the surrounding evidence.

## Day 26 Detection Focus

* `4624` Successful Logon
* `4625` Failed Logon
* `4672` Special Privileges
* Logon Types
* Brute-Force Detection
* Password Spraying
* Authentication Timeline
* Authentication Correlation

