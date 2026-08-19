# Day 26 - Brute Force Hunting

## Overview

Brute-force hunting identifies repeated failed authentication attempts against the same account.

Focus areas:

* Target account
* Source IP
* Failure count
* Time pattern
* Possible successful login

## Authentication Event

Windows Event ID `4625` represents a failed logon.

```text id="1f5x8k"
event_id = 4625
user     = Administrator
src_ip   = 10.49.108.50
action   = failed_logon
```

## Basic Failed-Logon Search

```spl id="6m2q9v"
index=main event_id=4625
| table _time user src_ip event_id action
| sort _time
```

## Count Failed Logons

```spl id="3k7p1d"
index=main event_id=4625
| stats count by user src_ip
| sort - count
```

Groups failures by **user + source IP**.

## Brute-Force Detection

```spl id="8v4n2x"
index=main event_id=4625
| stats count by user src_ip
| where count >= 3
```

Detection logic:

```text id="5r9c3m"
Same User
    +
Same Source IP
    +
3+ Failed Logons
    ↓
Possible Brute Force
```

The threshold is an investigation trigger, not proof of compromise.

## Controlled Lab Simulation

The available dataset did not contain enough real `4625` events for practical testing, so controlled events were simulated.

Example:

```text id="7q2m6v"
User       : Administrator
Source IP  : 10.49.108.50
Event ID   : 4625 × 5
```

### Simulated Detection

```spl id="4x8n1k"
| makeresults count=5
| eval event_id=4625
| eval user="Administrator"
| eval src_ip="10.49.108.50"
| eval action="failed_logon"
| stats count by user src_ip
| where count >= 3
```

Expected result:

```text id="2p6v9m"
user          src_ip         count
Administrator 10.49.108.50   5
```

## Time-Based Detection

Five failures within minutes are more relevant than five failures spread across hours.

A controlled time sequence can be created with:

```spl id="9c3k7x"
| streamstats count as n
| eval _time=now()-(n*60)
```

Five-minute bucket example:

```spl id="6v1m8q"
| bin _time span=5m
| stats count by _time user src_ip
| where count >= 3
```

`bin` uses fixed time boundaries, so bucket-based detection should be tested carefully when tuning alerts.

## Investigation Questions

When a brute-force alert fires:

* Who is being targeted?
* What is the source IP?
* How many failures occurred?
* How quickly did they occur?
* Is the account privileged?
* Is the source expected?
* Did authentication eventually succeed?
* What happened afterward?

## Failed → Successful Pattern

```text id="3x7n5p"
4625
  ↓
4625
  ↓
4625
  ↓
4624
```

Correlate:

**User + Source IP + Time + Event ID + Logon Type + Post-Authentication Activity**

## Brute Force vs Password Spraying

**Brute Force**

```text id="8m2q6r"
One Source
    ↓
One Account
    ↓
Many Password Attempts
```

**Password Spraying**

```text id="1v5k9x"
One Source
    ↓
Many Accounts
    ↓
Failed Authentication
```

## Analyst Principle

Do not label activity **"Confirmed brute force"** from a threshold alone.

Use:

> Multiple failed authentication attempts were observed against the same account from the same source and require investigation.

Then validate the surrounding evidence.

## Day 26 Outcome

Covered:

* `4625` identification
* Failed-login counting
* User/source grouping
* Threshold detection
* Time-window analysis
* Controlled simulation
* Failed-to-successful correlation

## Key Takeaway

```text id="7q4m2z"
Repeated Failures
       ↓
Same User + Source
       ↓
Time Context
       ↓
Threshold
       ↓
Correlation
       ↓
Investigation
```

**A brute-force alert is a starting point for investigation, not the final conclusion.**

