# Active Directory - AS-REP Roasting Investigation

## Status

**IN PROGRESS**

This section documents the investigation that was started during Day 37.

The final answer is intentionally not recorded because the required evidence still needs to be examined manually.

## Lab Context

The exercise presents a scenario involving possible persistence through creation of a new remote-SSH user on an Ubuntu server and then moves into Active Directory/Kerberos detection content.

The separate AS-REP Roasting exercise asks the analyst to inspect a file on the target environment.

## Evidence Location

The lab indicates:

```text
Desktop/Evidence/Security-DC
```

## Target

The target address used during the exercise was:

```text
10.129.185.214
```

## Detection Event

The relevant Windows Security event is:

```text
Event ID: 4768
```

## Relevant Fields

The lesson identifies:

```text
Pre-Authentication Type: 0
Ticket Encryption Type: 0x17
```

## Why the Fields Matter

The exercise uses the combination of the event type and these field values to identify the relevant Kerberos activity.

## Manual Procedure

### Step 1

Open the supplied evidence file.

### Step 2

Locate Event ID `4768`.

### Step 3

Inspect the event details.

### Step 4

Find the event where pre-authentication is `0`.

### Step 5

Confirm encryption type `0x17`.

### Step 6

Read the account associated with that event.

### Step 7

Read the timestamp from the same event.

### Step 8

Enter the values using the lab's exact answer format.

## Important Distinction

`4768` is the Event ID.

It is not the answer when the question asks for the targeted account.

The username must be extracted from the event.

## Current State

The evidence still needs to be accessed through the intended HTB environment.

No guessed username or timestamp is stored here.

## Completion Criteria

The investigation can be marked complete after documenting:

- Targeted account
- Exact timestamp
- Event ID
- Pre-authentication type
- Ticket encryption type
- Supporting screenshot

## Analyst Discipline

Do not convert an incomplete investigation into a completed result just because the event type is known.

The final account and timestamp must come from the evidence.
