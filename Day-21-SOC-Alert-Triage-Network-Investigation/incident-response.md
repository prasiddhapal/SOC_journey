# Day 21 - Incident Response

## Objective

Document the response actions that follow a confirmed malicious alert.

## Response Workflow

```text
Confirm Alert
     ↓
Assess Impact
     ↓
Contain
     ↓
Investigate
     ↓
Eradicate
     ↓
Recover
     ↓
Document
```

## Immediate Containment

Depending on the evidence:

- Isolate the affected endpoint
- Block malicious domain/IP
- Stop malicious processes
- Preserve relevant evidence
- Escalate when required

## Investigation

Confirm:

- Affected user
- Affected host
- Parent and child processes
- Malicious files
- Network connections
- Relevant IOCs
- Scope of activity

## Escalation

Escalate when:

- Impact is significant
- Malware execution is confirmed
- Persistence is identified
- Credentials may be compromised
- Multiple endpoints are affected
- L2/L3 expertise is required

## Documentation

Record:

- What happened
- Evidence collected
- Timeline
- Verdict
- Severity
- Actions taken
- Remaining uncertainty

## Key Lesson

> **Containment should reduce attacker access while preserving the evidence required for investigation.**

## Status

**Completed ✅**
