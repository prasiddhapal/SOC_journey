# Day 21 - SOC Interview Questions

## Technical Questions

### 1. What is SOC alert triage?

Alert triage is the process of validating, prioritising, investigating, and classifying security alerts.

### 2. Does Critical severity always mean True Positive?

No. Severity determines investigation priority. Evidence determines the final verdict.

### 3. What is PID and PPID?

**PID** identifies a process.  
**PPID** identifies its parent process.

### 4. Why is WINWORD.EXE spawning PowerShell suspicious?

It can indicate a malicious document triggering PowerShell, especially with encoded, hidden, or bypassed execution.

### 5. What is Event ID 4688?

Windows Process Creation logging used to investigate process execution and related process information.

### 6. What is PowerShell Event ID 4104?

PowerShell Script Block Logging used to investigate PowerShell script activity when logging is configured.

### 7. Does HTTPS traffic prove C2?

No. HTTPS is commonly legitimate. C2 requires additional evidence such as communication patterns, infrastructure reputation, or command-and-control behavior.

## HR Questions

### 8. Why do you want to work in a SOC?

I enjoy security investigation and problem-solving. I want to build practical skills in monitoring, investigation, incident response, and continuous learning.

### 9. How do you handle an unfamiliar alert?

I would first understand the alert, identify the affected user and host, collect relevant telemetry, correlate the evidence, and escalate when required.

### 10. How do you handle mistakes during an investigation?

I would acknowledge the mistake, verify the evidence, correct the analysis, document what changed, and use the experience to improve future investigations.

## Key Interview Principle

> **Do not guess. Explain what the evidence proves, what remains unknown, and what you would investigate next.**

## Status

**Completed ✅**
