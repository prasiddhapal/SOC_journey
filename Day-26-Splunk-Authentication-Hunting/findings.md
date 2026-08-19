# Day 26 - Authentication Hunting Findings

## Overview

Day 26 focused on **Windows authentication hunting using Splunk**.

The objective was to investigate authentication events, identify suspicious patterns, and correlate activity.

## Observed Authentication

The lab contained one successful authentication:

```text id="4m6c0v"
Event ID   : 4624
User       : Administrator
Source IP  : 10.49.108.37
Logon Type : 3
Action     : successful_logon
```

## Logon Type Finding

The event contained:

```text id="5b6q2j"
logon_type = 3
```

**Logon Type 3** represents a **Network Logon**.

It does not represent three login attempts.

## Failed Authentication

No `4625` failed-logon events were observed in the available lab dataset.

```text id="8s3x0m"
4625 = Not observed
```

This does **not** prove that failed authentication never occurred. It only describes the available dataset.

## Privileged Authentication

A search for Event ID `4672` was performed.

```text id="q3z8am"
4672 = Not observed
```

No special-privilege events were available for correlation.

## Field Discovery

`fieldsummary` was used to identify available authentication fields.

Important fields included:

```text id="7z5q6f"
_time
user
src_ip
dest_ip
event_id
logon_type
action
host
source
sourcetype
```

The field discovery process confirmed the correct field name:

```text id="3j2v6s"
logon_type
```

## Brute-Force Simulation

Because real `4625` events were unavailable, controlled simulated events were used for detection practice.

Example:

```text id="r8h4yx"
User       : Administrator
Source IP  : 10.49.108.50
Event ID   : 4625 × 5
```

A threshold of **3 failed logons** produced a detection.

## Password-Spraying Simulation

A controlled simulation used source IP `10.49.108.48` against multiple accounts:

```text id="5r7k2p"
Administrator
harry
honey
famous
khushi
god
```

Detection result:

```text id="2t0j5c"
unique_users = 6
count = 6
```

This demonstrated the password-spraying pattern:

**One source IP → multiple targeted users → failed authentication**

## Failed → Successful Simulation

A controlled sequence demonstrated:

```text id="7n5x9a"
4625
  ↓
4625
  ↓
4625
  ↓
4624
```

The events used the same account and source IP.

This demonstrated how repeated failures followed by successful authentication can increase investigation priority.

## Key SOC Lessons

* Validate the actual data before reaching conclusions.
* Use `fieldsummary` when field names are uncertain.
* `logon_type=3` means Network Logon.
* `count` represents the number of matching events.
* `dc(user)` represents the number of distinct users.
* Brute force and password spraying are different patterns.
* A detection is not automatically proof of compromise.
* Missing events should be documented as **not observed**.

## Investigation Model

```text id="q0y4vk"
Authentication Event
        ↓
User + Source IP
        ↓
Logon Type
        ↓
Failure Pattern
        ↓
Time Correlation
        ↓
Post-Authentication Activity
        ↓
Risk Assessment
```

## Final Finding

The available dataset showed a successful **Network Logon** for the `Administrator` account from `10.49.108.37`.

Controlled simulations were used to practice:

* Brute-force detection
* Password-spraying detection
* Failed → successful authentication correlation

## Day 26 Status

**Authentication Hunting - Completed**

