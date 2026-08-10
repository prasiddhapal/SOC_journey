
---

## `incident-response.md`

```markdown
# Incident Response

## Incident

**Type:** Phishing  
**Severity:** Medium  
**Status:** Investigation completed with limited telemetry

## Immediate Actions

1. Quarantine the phishing email.
2. Block the malicious domain.
3. Check whether other users received the same email.
4. Investigate endpoint activity for downloads or execution.
5. Reset credentials if credential submission is confirmed.
6. Monitor for related activity.

## Evidence Status

```text
Phishing Email       → Confirmed
Malicious URL        → Confirmed
URL Access           → Confirmed
File Download        → Not Confirmed
Payload Execution    → Not Confirmed
Credential Theft     → Not Confirmed
Endpoint Compromise  → Not Confirmed
