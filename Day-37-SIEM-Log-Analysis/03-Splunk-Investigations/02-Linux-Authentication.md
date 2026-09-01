# 02 - Linux Authentication Investigation

## Search Context

The Linux investigation used `auth.log` with the `linux_secure` sourcetype.

## Example Search

```spl
index=task5 source="auth.log" "Failed password for jack-brown"
```

## Purpose

This search identifies failed password events involving the specified account.

## What to Examine

For each relevant event, inspect:

- Timestamp
- Username
- Source IP
- Source port
- Authentication service
- Result

## Successful Authentication

A successful authentication event should be compared against previous failed attempts.

The comparison can establish whether failures preceded a successful login.

## Timeline Questions

Ask:

1. When did the failures begin?
2. How many failures occurred?
3. Did a successful login follow?
4. Which source IP was involved?
5. Was privileged activity observed afterwards?

## Evidence

Do not count events from memory.

Use the returned events.

Record exact timestamps.

## Analyst Conclusion

The final conclusion should distinguish:

- Observed authentication activity
- Correlated activity
- Interpretation

This keeps the investigation evidence-based.
