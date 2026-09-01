# Linux Authentication Logs

## Log Source

The practical investigation used:

```text
source=auth.log
sourcetype=linux_secure
```

## Authentication Evidence

Linux authentication logs can show:

- Failed password attempts
- Successful authentication
- Session creation
- Session closure
- Privileged activity

## Failed Attempts

Repeated failures may require investigation.

The analyst should identify:

- Account
- Source IP
- Timestamp
- Authentication method

## Successful Login

A successful login following repeated failures can be significant.

However, the analyst should verify the exact event rather than assuming the reason.

## Sudo

Sudo activity provides additional context.

It can show when a user obtained elevated privileges and which commands were executed.

## Investigation Timeline

A useful timeline can be:

1. Failed authentication.
2. More failed authentication.
3. Successful authentication.
4. Privilege escalation.
5. Command execution.
6. Session closure.

The actual order must be established from the event timestamps.

## Documentation

Record exact values from the logs.

Avoid replacing observed values with assumptions.
