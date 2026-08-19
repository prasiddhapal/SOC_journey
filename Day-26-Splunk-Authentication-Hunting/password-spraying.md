# Day 26 - Password Spraying

## Overview

Password spraying is an authentication attack pattern where one source attempts authentication against multiple accounts.

**Key pattern:**

```text id="5k2m8q"
One Source IP
      ↓
Multiple Users
      ↓
Failed Authentication
```

## Authentication Event

Windows Event ID `4625` represents failed authentication.

```text id="8v4n1p"
event_id = 4625
src_ip   = 10.49.108.48
action   = failed_logon
```

## Password Spraying vs Brute Force

### Password Spraying

```text id="2m7x5c"
One Source
    ↓
Multiple Users
    ↓
Failed Authentication
```

### Brute Force

```text id="9q3v6k"
One Source
    ↓
One User
    ↓
Many Failed Attempts
```

The number of targeted users is an important distinguishing factor.

## Basic Search

```spl id="6p1r8z"
index=main event_id=4625
| table _time user src_ip event_id action
| sort _time
```

## Source-to-User Analysis

```spl id="4x9m2v"
index=main event_id=4625
| stats count by src_ip user
| sort - count
```

Shows which accounts are being targeted by each source.

## Distinct User Detection

```spl id="7k5q1n"
index=main event_id=4625
| stats dc(user) as unique_users count by src_ip
| where unique_users >= 3
```

`dc(user)` returns the number of distinct users.

### Detection Logic

```text id="3v8m6x"
4625 Failed Logon
       ↓
Group by Source IP
       ↓
Count Unique Users
       ↓
3+ Users
       ↓
Possible Password Spraying
```

The threshold is an investigation trigger, not proof of compromise.

## Lab Simulation

The available dataset did not contain enough real `4625` events for practical testing, so controlled events were simulated.

**Source:**

```text id="1q6p4z"
10.49.108.48
```

**Targeted accounts:**

```text id="8m3v7c"
Administrator
harry
honey
famous
khushi
god
```

Simulation result:

```text id="5x9k2r"
unique_users = 6
count = 6
```

## Detection Example

```spl id="0v6m3q"
| makeresults count=6
| streamstats count as n
| eval src_ip="10.49.108.48"
| eval user=case(
    n=1,"Administrator",
    n=2,"harry",
    n=3,"honey",
    n=4,"famous",
    n=5,"khushi",
    true(),"god"
)
| eval event_id=4625
| eval action="failed_logon"
| stats dc(user) as unique_users count by src_ip
| where unique_users >= 3
```

## SOC Investigation

When the alert fires, investigate:

* Source IP
* Targeted accounts
* Number of failures
* Time period
* Account importance
* Whether authentication later succeeded
* Activity after successful authentication

## Important Principle

A password-spraying detection does **not automatically prove compromise**.

```text id="6n2q8v"
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

## Day 26 Outcome

Password-spraying detection was successfully simulated and investigated using Splunk SPL.

### Key Takeaway

```text id="4r7m1x"
One Source
    +
Multiple Accounts
    +
Failed Authentication
    =
Possible Password Spraying
```

**Correlate the evidence before reaching a conclusion.**

