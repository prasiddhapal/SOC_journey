# 🛡️ SOC Journey

### Practical Blue Team & Security Operations Portfolio

> Building hands-on SOC investigation, detection, incident response, and AI-assisted security operations skills through practical labs and documented investigations.

![Linux](https://img.shields.io/badge/Linux-Security-blue)
![Blue Team](https://img.shields.io/badge/Blue%20Team-SOC-success)
![AI](https://img.shields.io/badge/AI-Assisted%20SOC-purple)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)
![Focus](https://img.shields.io/badge/Focus-SOC%202026-red)

---

## About

This repository is a practical security operations portfolio documenting the progression from Linux and networking fundamentals into hands-on SOC investigation.

The focus is on **investigating security events, understanding evidence, correlating telemetry, and making defensible security decisions**.

Current areas include:

* Linux security and administration
* Log analysis
* Network investigation
* SOC alert triage
* Endpoint and process investigation
* IOC analysis
* Phishing investigation
* Incident response
* Threat hunting fundamentals
* AI-assisted SOC investigation

---

## Current Capabilities

### 🐧 Linux & Systems

* Linux administration
* User and permission management
* Process investigation
* Authentication analysis
* Service management
* System and security logs
* Linux networking
* Bash fundamentals

### 🌐 Network Investigation

* TCP/IP fundamentals
* DNS investigation
* HTTP/HTTPS analysis
* Socket analysis
* Source/destination analysis
* Network and proxy correlation
* IOC investigation

### 🛡️ SOC Operations

* Alert triage
* Alert prioritisation
* True Positive / False Positive analysis
* Process and endpoint investigation
* Log correlation
* Timeline construction
* IOC extraction
* Incident response decisions
* Evidence-based reporting

### 🤖 AI-Assisted Security Operations

AI is used as an investigation assistant for:

* Log analysis
* Command analysis
* SIEM query generation
* IOC enrichment
* Timeline assistance
* Investigation pivots
* MITRE ATT&CK research
* Documentation

**AI-generated findings are validated against security telemetry before being treated as conclusions.**

---

## Investigation Methodology

The repository follows a repeatable investigation workflow:

```text
Alert
  ↓
Triage
  ↓
Evidence Collection
  ↓
Endpoint / Process Analysis
  ↓
Network Analysis
  ↓
Log Correlation
  ↓
IOC Investigation
  ↓
Timeline
  ↓
Verdict
  ↓
Response
  ↓
Documentation
```

### Core Principle

> **Evidence first. Conclusions second.**

---

## Practical Investigations

### 🔎 Phishing Investigation

Investigated a simulated phishing incident involving:

* Email sender and domain analysis
* Malicious URL investigation
* IOC extraction
* Browser activity
* Proxy/log correlation
* Endpoint activity
* Severity assessment
* Incident response recommendations

### 🛡️ SOC Alert Triage

Hands-on SOC alert investigation covering:

* Alert properties
* Alert prioritisation
* True Positive / False Positive classification
* Process investigation
* PID / PPID analysis
* PowerShell investigation
* Network correlation
* DNS investigation
* IOC analysis
* Incident response

**Platform:** TryHackMe SOC L1 Alert Triage

---

## Investigation Examples

### Suspicious Process Chain

```text
WINWORD.EXE
     ↓
powershell.exe
     ↓
Encoded / Hidden Command
     ↓
External HTTPS Connection
     ↓
update.ps1
```

### Network Correlation

```text
Process
  ↓
DNS Query
  ↓
Resolved IP
  ↓
Network Connection
  ↓
Proxy Request
  ↓
Downloaded File
```

### AI-Assisted Investigation

```text
Security Alert
      ↓
AI-Assisted Analysis
      ↓
Investigation Hypothesis
      ↓
Real Telemetry
      ↓
Human Validation
      ↓
Final Decision
```

---

## Tools & Technologies

### Current

* Linux
* Bash
* Git
* GitHub
* TryHackMe
* OpenSSH
* UFW
* `grep`
* `awk`
* `sed`
* `journalctl`
* `ps`
* `top`
* `ss`
* `curl`
* `dig`
* `tcpdump`

### Building Toward

* Windows Security
* PowerShell
* Splunk
* Microsoft Sentinel
* Wazuh
* Sysmon
* Wireshark
* Zeek
* Suricata
* Velociraptor
* Sigma
* MITRE ATT&CK

---

## Repository Structure

```text
SOC_Journey/

├── Linux/
├── Windows/
├── Active-Directory/
├── SIEM/
├── Threat-Hunting/
├── Detection-Engineering/
├── Incident-Response/
├── Malware-Analysis/
├── Cloud-Security/
├── AI-for-SOC/
└── Projects/
```

Each practical module is documented with relevant:

```text
README.md
notes.md
commands.md
investigation.md
incident-response.md
iocs.md
interview-questions.md
Screenshots/
```

The exact files vary depending on the investigation.

---

## Current Progress

| Area                      | Status |
| ------------------------- | :----: |
| Linux Fundamentals        |    ✅   |
| Linux Administration      |    ✅   |
| Linux Security            |    ✅   |
| Linux Log Analysis        |    ✅   |
| Linux Networking          |    ✅   |
| Network Investigation     |    ✅   |
| Phishing Investigation    |    ✅   |
| SOC Alert Triage          |    ✅   |
| Process Investigation     |    ✅   |
| IOC Analysis              |    ✅   |
| Incident Investigation    |    ✅   |
| AI-Assisted Investigation |    ✅   |
| Windows Security          |   🔄   |
| PowerShell                |   🔄   |
| SIEM                      |    ⏳   |
| Threat Hunting            |    ⏳   |
| Detection Engineering     |    ⏳   |
| Incident Response         |   🔄   |
| Active Directory          |    ⏳   |
| Malware Analysis          |    ⏳   |
| Cloud Security            |    ⏳   |

---

## Roadmap

```text
Linux & Networking
        ↓
SOC Fundamentals
        ↓
Windows Security
        ↓
SIEM
        ↓
Threat Hunting
        ↓
Detection Engineering
        ↓
Incident Response
        ↓
Advanced Blue Team
        ↓
AI-Augmented SOC Operations
```

The roadmap is intentionally practical: each major stage is supported by hands-on investigation rather than only theoretical study.

---

## Documentation Standard

Every investigation aims to answer:

```text
What happened?
     ↓
What evidence supports it?
     ↓
How was it investigated?
     ↓
What is confirmed?
     ↓
What remains unknown?
     ↓
What should happen next?
```

This keeps the repository focused on **analytical reasoning and evidence**, rather than simply recording completed exercises.

---

## Current Objective

Build practical, job-ready SOC investigation capability for **2026 SOC**.

The immediate focus is progressing from Linux-based security investigations into:

* Windows telemetry
* SIEM operations
* Threat hunting
* Detection engineering
* Incident response
* AI-assisted security operations

---

## Contact

* **LinkedIn:** [www.linkedin.com/in/prasiddha-pal](http://www.linkedin.com/in/prasiddha-pal)
* **GitHub:** github.com/prasiddhapal

---

> **Trust the evidence. Validate the findings. Question every assumption.**
