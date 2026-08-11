# Day 21 - SOC Notes

## 1. Alert Triage

Alert triage means validating an alert, understanding its context, prioritising it, and deciding the appropriate response.

### Basic Workflow

Alert → Validate → Investigate → Correlate → Verdict → Severity → Response

## 2. Alert Prioritisation

Prioritise alerts using:

- Severity
- Alert status
- Investigation ownership
- Time
- Potential impact

**Important:** High or Critical severity does not automatically mean True Positive.

## 3. True Positive vs False Positive

**True Positive:** Evidence confirms malicious or unwanted activity.

**False Positive:** The alert triggered, but investigation shows legitimate activity.

### Practical Examples

- Legitimate GitHub repository access by a developer → False Positive
- Malicious double-extension executable download → True Positive

## 4. Process Investigation

Important process information:

- Process name
- PID
- PPID
- Parent process
- Child process
- User
- Host
- Command line
- Executable path

### Suspicious Example

WINWORD.EXE → PowerShell → Encoded Command

Important indicators include:

- `-ExecutionPolicy Bypass`
- `-WindowStyle Hidden`
- `-EncodedCommand`

## 5. Network Correlation

Correlate:

Process → DNS → IP → Port → Proxy → File

Investigate:

- Source IP
- Destination IP
- Domain
- Port
- Protocol
- DNS activity
- Proxy activity
- Connection timing

HTTPS traffic alone does not prove malicious activity or C2.

## 6. AI-Assisted SOC

AI can help with:

- Command analysis
- SIEM query generation
- IOC extraction
- Timeline creation
- MITRE ATT&CK suggestions
- Investigation pivots

### Core Rule

> AI generates hypotheses. Evidence generates conclusions.

Always validate AI output against actual telemetry.

## Key Lesson

**Severity determines priority. Evidence determines the verdict.**
