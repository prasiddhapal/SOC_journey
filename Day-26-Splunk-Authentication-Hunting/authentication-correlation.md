# Day 26 - Authentication Correlation

## Overview

Authentication correlation connects multiple Windows authentication events to understand the sequence and context of user activity.

The goal is to determine whether authentication activity requires further investigation.

## Core Events

| Event ID | Meaning                     |
| -------- | --------------------------- |
| `4624`   | Successful Logon            |
| `4625`   | Failed Logon                |
| `4672`   | Special Privileges Assigned |

## Core Fields

```text id="7q2m5x"
_time
user
src_ip
dest_ip
event_id
logon_type
action
```

## Basic Authentication Timeline

```spl id="4v8n1k"
index=main
| sort _time
| table _time user src_ip event_id logon_type action
```

Provides a chronological view of authentication activity.

## Previous Event Correlation

```spl id="9m3x6q"
index=main
| sort _time
| streamstats current=f last(event_id) as previous_event
| table _time user src_ip event_id previous_event
```

`streamstats` allows the current event to be compared with the previous event.

## Time Difference

```spl id="2k7p4v"
index=main
| sort _time
| streamstats current=f last(_time) as previous_time
| eval time_diff=_time-previous_time
| table _time user event_id previous_time time_diff
```

`time_diff` represents the time between the current and previous events.

## Failed → Successful Pattern

A useful investigation pattern is:

```text id="6x1q8m"
4625
  ↓
4625
  ↓
4625
  ↓
4624
```

Repeated failed authentication followed by a successful logon can increase investigation priority.

## Investigation Logic

```text id="3v9m5k"
Failed Logons
      ↓
Same User?
      ↓
Same Source IP?
      ↓
Short Time Window?
      ↓
Successful Logon?
      ↓
Investigate
```

## Controlled Simulation

The lab did not contain enough real failed-logon events, so controlled events were simulated.

```text id="8q4n2p"
User      : Administrator
Source IP : 10.49.108.48

4625 → failed
4625 → failed
4625 → failed
4624 → successful
```

## Simulated Timestamp Logic

```spl id="5m7x1c"
| streamstats count as n
| eval _time=now()-(4-n)*30
```

Creates four test events approximately 30 seconds apart:

```text id="1p6v9k"
n=1 → 90 seconds ago
n=2 → 60 seconds ago
n=3 → 30 seconds ago
n=4 → current time
```

This was used only for controlled lab simulation.

## Stronger Correlation

A failed authentication followed by a successful logon becomes more interesting when there is:

**Same User + Same Source IP + Short Time Interval + `4625 → 4624`**

## Post-Authentication Investigation

After a successful logon, investigate what happened next:

```text id="7k3q8v"
4624
  ↓
Process Execution
  ↓
Command Activity
  ↓
Network Activity
```

The lab showed subsequent process activity including PowerShell and `cmd.exe /c whoami`.

Detailed process analysis belongs to **Day 27**.

## Analyst Principle

Correlation provides context, but it does **not prove malicious activity**.

Validate:

* Source IP
* Account
* Time
* Logon Type
* Authentication pattern
* Post-authentication activity

## Evidence Discipline

```text id="4x8m2q"
Observed
   ↓
Correlated
   ↓
Investigated
   ↓
Assessed
```

Do not turn missing events into conclusions.

## Day 26 Outcome

Authentication correlation was practiced using:

* `4624`
* `4625`
* Source IP
* User
* Time differences
* `streamstats`
* Controlled event simulation

## Key Takeaway

```text id="9v5k1m"
Authentication Events
        ↓
Timeline
        ↓
Correlation
        ↓
Context
        ↓
Investigation
```

Authentication correlation helps transform individual events into meaningful SOC investigation context.

