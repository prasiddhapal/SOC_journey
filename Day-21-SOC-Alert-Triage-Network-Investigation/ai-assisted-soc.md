# Day 21 - SOC Alert Triage

## Objective

Practice validating, prioritising, investigating, and classifying SOC alerts using a SIEM-style environment.

## Triage Workflow

```text
Alert
  ↓
Validate
  ↓
Identify User / Host
  ↓
Prioritise
  ↓
Investigate
  ↓
Correlate Evidence
  ↓
True Positive / False Positive
  ↓
Assess Severity
  ↓
Respond / Escalate
  ↓
Close
```

## Initial Alert Checks

Review:

- Alert name
- Severity
- Timestamp
- User
- Host
- Source / destination
- Alert description
- Current status
- Existing assignee

## Alert Prioritisation

Prioritise alerts using:

1. Investigation status
2. Severity
3. Time and context
4. Potential impact

**Important:** Critical severity means higher investigation priority, not automatic confirmation of malicious activity.

## Investigation

Correlate:

```text
User
 ↓
Host
 ↓
Process
 ↓
PID / PPID
 ↓
File Activity
 ↓
Network Activity
 ↓
Related Events
```

Look for supporting evidence before making a verdict.

## True Positive

A **True Positive** is an alert where investigation confirms malicious or unwanted activity.

Example:

```text
Suspicious file
   ↓
Malicious source
   ↓
Endpoint evidence
   ↓
Confirmed activity
   ↓
True Positive
```

## False Positive

A **False Positive** occurs when an alert triggers but investigation shows legitimate or benign activity.

Examples from the lab included:

- Legitimate developer access to GitHub
- Legitimate Zoom network activity

## Severity

Severity should consider:

- Potential impact
- Scope
- Confidence
- User privilege
- Persistence
- Data exposure

Do not automatically equate:

```text
Critical Alert = Critical Incident
```

## AI-Assisted Triage

AI can help with:

- Alert summaries
- SIEM query generation
- IOC extraction
- Timeline analysis
- Investigation pivots
- MITRE ATT&CK suggestions

### AI Validation Rule

```text
AI Hypothesis
     ↓
Required Evidence
     ↓
Real Telemetry
     ↓
Analyst Verification
     ↓
Final Decision
```

> **AI can accelerate investigation, but evidence determines the conclusion.**

## Key Lessons

- Do not judge an alert only by its title.
- Severity determines priority, not the verdict.
- Correlate multiple telemetry sources.
- Separate confirmed facts from assumptions.
- Document the reasoning behind the final decision.

## Status

**Day 21 - Completed ✅**
