# Windows Security Events

## Overview

Windows Security logs provide authentication and security-related telemetry.

## Event IDs

An Event ID identifies the type of event.

It should not automatically be treated as the answer to an investigation question.

## Kerberos Event 4768

The Active Directory lesson identifies Event ID `4768` as a Kerberos ticket-request event.

The relevant event details should be inspected manually.

## AS-REP Indicators

The lesson identifies:

```text
Pre-Authentication Type: 0
Ticket Encryption Type: 0x17
```

These fields are important for the lab investigation.

## Investigation Method

1. Search for Event ID 4768.
2. Inspect event details.
3. Identify the account.
4. Confirm the pre-authentication field.
5. Confirm the encryption field.
6. Record the timestamp.
7. Preserve the event as evidence.

## Important

Event ID `4768` is not the account name.

The account must be read from the matching event.

## Timeline

The event timestamp should be recorded exactly as presented by the lab unless the question specifies another format.

## Evidence Standard

Use the event that matches all required indicators.

Do not select an event based on Event ID alone.
