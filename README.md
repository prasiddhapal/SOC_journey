# SOC Analyst Journey

> A hands-on cybersecurity portfolio focused on **SOC operations, SIEM investigation, detection engineering, threat hunting, DFIR, network security, and incident response**.

[![Status](https://img.shields.io/badge/Status-Active-brightgreen)](https://github.com/prasiddhapal/SOC_journey)
[![Progress](https://img.shields.io/badge/Progress-Day%2044-blue)](https://github.com/prasiddhapal/SOC_journey)
[![Focus](https://img.shields.io/badge/Focus-SOC%20%7C%20Blue%20Team%20%7C%20DFIR-informational)](https://github.com/prasiddhapal/SOC_journey)

## Overview

This repository documents a structured **hands-on SOC Analyst development journey**. Each day focuses on a practical security capability and records the investigation process, evidence, findings, validation, and lessons learned.

The goal is to develop the ability to:

- Triage and investigate security alerts
- Correlate endpoint, identity, network, and SIEM telemetry
- Distinguish normal activity from meaningful anomalies
- Build and validate detection logic
- Reconstruct attack timelines
- Perform evidence-driven DFIR investigations
- Communicate findings clearly and defensibly

**Current progress:** Day 44  
**Status:** Active  
**Author:** [Prasiddha Pal](https://github.com/prasiddhapal)

---

## Quick Start

```bash
git clone https://github.com/prasiddhapal/SOC_journey.git
cd SOC_journey
```

Choose a completed investigation:

```bash
cd Day-44-Active-Directory-Threat-Hunting-Kerberos-Anomaly-Validation
```

Recommended workflow:

```text
README
  ↓
Commands / Queries
  ↓
Investigation
  ↓
Evidence
  ↓
Findings
  ↓
Validation
  ↓
Lessons Learned
```

---

## Investigation Philosophy

Every investigation follows the same analyst discipline:

```text
Evidence
   ↓
Observation
   ↓
Hypothesis
   ↓
Correlation
   ↓
Confidence
   ↓
Conclusion
   ↓
Response / Detection
```

### Core Principles

**Evidence before conclusions**  
Findings are supported by observable logs, artifacts, queries, or other evidence.

**Correlation over isolated events**  
Identity, endpoint, network, and SIEM telemetry are correlated wherever possible.

**Suspicious is not confirmed**  
The documentation separates observations, hypotheses, confidence, and confirmed findings.

**Baseline before anomaly**  
Normal account, host, service, authentication, and network behavior provides context for hunting.

**Reproducibility**  
Commands and SIEM queries are documented so investigations can be repeated in authorized lab environments.

---

## Skills Developed

### SOC Operations
- Alert triage
- Incident investigation
- Event correlation
- False-positive validation
- Evidence collection
- Investigation reporting

### SIEM & Detection Engineering
- Splunk / SPL
- IBM QRadar
- Log filtering and correlation
- Authentication hunting
- Baseline and anomaly analysis
- Detection logic
- Detection validation and tuning

### Windows & Identity
- Windows Security Events
- Sysmon
- PowerShell
- Active Directory
- Kerberos
- NTLM
- Account and group investigation
- Privileged-account analysis

### Network Security
- TCP/IP
- DNS
- HTTP/S
- SMB
- Wireshark
- TShark
- PCAP analysis
- Reconnaissance
- C2 investigation

### DFIR & Malware Analysis
- Volatility 3
- Memory forensics
- Process investigation
- File and artifact analysis
- JavaScript/browser-extension analysis
- Credential-theft investigation
- Keylogging and exfiltration analysis
- IOC extraction

### Threat Intelligence
- VirusTotal
- MalwareBazaar
- ThreatFox
- Hash, IP, domain, and infrastructure analysis
- MITRE ATT&CK

### Cloud Security
- AWS forensics fundamentals
- CloudTrail fundamentals
- IAM fundamentals
- Cloud identity investigation

---

## Journey Progress

### Days 1–19 | Linux Security Foundations

| Day | Focus |
|---|---|
| 01 | Linux Authentication Logs |
| 02 | SSH Authentication Investigation |
| 03 | SSH Brute-Force Investigation |
| 04 | Linux Users & Permissions |
| 05 | Process Management |
| 06 | Linux Services & Logs |
| 07 | Linux Networking for SOC Analysts |
| 08 | Linux Network Analysis |
| 09 | Linux Firewall & System Security |
| 10 | Linux File Investigation & Integrity |
| 11 | Linux Archive & Compression |
| 12 | Linux Special Permissions & Ownership |
| 13 | Linux Capabilities & Privilege Escalation |
| 14 | Linux Capability Abuse & SOC Investigation |
| 15 | Linux Log Hunting & IOC Correlation |
| 16 | Linux Logging & Investigation |
| 17 | Advanced Linux Commands |
| 18 | Linux Process & Network Investigation |
| 19 | Linux Authentication & User Activity |

### Days 20–30 | SOC Operations & SIEM

| Day | Focus |
|---|---|
| 20 | SOC Phishing Investigation |
| 21 | SOC Alert Triage & Network Investigation |
| 22 | Windows Event Investigation |
| 23 | Splunk Investigation |
| 24 | Splunk Detection |
| 25 | Splunk Transaction Analysis |
| 26 | Splunk Authentication Hunting |
| 27 | Splunk Detection Engineering |
| 28 | Splunk Context-Aware Detection |
| 29 | Splunk Alert Triage |
| 30 | Splunk Correlation Investigations |

### Days 31–39 | DFIR, Threat Intelligence & Enterprise Telemetry

| Day | Focus |
|---|---|
| 31 | Memory Forensics |
| 32 | Threat Intelligence & Wireshark |
| 33 | AWS Cloud Forensics & Phishing |
| 34 | Windows Logging, Sysmon & PowerShell |
| 35 | Linux Logging & SOC |
| 36 | Network Traffic Analysis |
| 37 | SIEM Log Analysis |
| 38 | Brutus Professional |
| 39 | QRadar 101 |

### Days 40–44 | Advanced Investigations & Identity

| Day | Focus |
|---|---|
| 40 | Lockdown — Multi-Stage DFIR Investigation |
| 41 | Browser Extension Malware Analysis & Covert Data Exfiltration |
| 42 | Active Directory Security & Windows Identity Investigation |
| 43 | Active Directory Monitoring & Kerberos Investigation |
| 44 | Active Directory Threat Hunting & Kerberos Anomaly Validation |

---

## Investigation Highlights

### Day 20 — SOC Phishing Investigation
Email analysis, URL extraction, IOC hunting, and investigation workflow.

### Day 21 — SOC Alert Triage
Alert validation, process/network correlation, evidence gathering, and response decisions.

### Day 34 — Windows Logging, Sysmon & PowerShell
Endpoint telemetry, process relationships, PowerShell analysis, and network correlation.

### Day 38 — Brutus Professional
Authentication abuse, persistence, privilege escalation, and timeline reconstruction.

### Day 39 — QRadar 101
Multi-source SIEM investigation across Windows, network, and application telemetry.

### Day 40 — Lockdown
PCAP reconnaissance → SMB → web shell → reverse shell → memory forensics → persistence → malware → C2.

### Day 41 — Browser Extension Malware Analysis
Credential theft → keylogging → AES encryption → Base64 → covert `<img>` exfiltration → anti-analysis.

### Day 44 — Active Directory Threat Hunting
Kerberos service-ticket baselining, rare-value hunting, source correlation, negative findings, and false-positive reduction.

---

## Investigation Methodology

A typical case follows:

```text
1. Alert / Hypothesis
      ↓
2. Evidence Collection
      ↓
3. Artifact Analysis
      ↓
4. Correlation
      ↓
5. Validation
      ↓
6. Scope & Impact
      ↓
7. ATT&CK Mapping
      ↓
8. Detection / Response
      ↓
9. Documentation
```

The workflow is iterative. A hypothesis can be strengthened, weakened, or rejected as new evidence appears.

---

## Documentation Standard

A completed module may contain:

```text
Day-XX-Topic/
├── README.md
├── commands.md
├── investigation.md
├── findings.md
├── validation.md
├── interview-questions.md
├── notes.md
└── Screenshots/
```

### README
Objectives, scenario, prerequisites, investigation overview, key findings, and attack flow.

### Commands / Queries
Reproducible terminal commands and SIEM queries.

### Investigation
Chronological reasoning, observations, hypotheses, evidence, and correlation.

### Findings
Executive summary, IOCs, ATT&CK mapping, false positives, impact, response, and lessons learned.

### Validation
Independent verification steps, expected results, negative tests, and detection validation.

### Screenshots
Meaningful evidence from the investigation. Completion badges are not a substitute for investigation evidence.

---

## Tool Stack

| Area | Tools / Frameworks |
|---|---|
| SIEM | Splunk, IBM QRadar |
| Network | Wireshark, TShark, tcpdump |
| Windows | Sysmon, PowerShell, Windows Event Logs |
| DFIR | Volatility 3 |
| Threat Intelligence | VirusTotal, MalwareBazaar, ThreatFox |
| Detection | SPL, MITRE ATT&CK |
| Linux | Bash, grep, awk, sed, journalctl, ps, ss |
| Security Testing | Nmap, Burp Suite, Metasploit, OWASP ZAP |
| Cloud | AWS, CloudTrail fundamentals, IAM fundamentals |
| Version Control | Git, GitHub |

Tools are included because they support investigation, detection, hunting, response, or interview readiness. Production experience is not claimed unless it was actually demonstrated hands-on.

---

## Next Phase

```text
Active Directory & Identity
        ↓
Kerberos / NTLM
        ↓
Privilege Escalation & Lateral Movement
        ↓
Windows Endpoint Detection
        ↓
Sigma / KQL
        ↓
Threat Hunting
        ↓
AWS / Entra Identity
        ↓
Incident Response
        ↓
SOC Capstone Investigations
        ↓
Job-Ready Assessment
```

The roadmap evolves based on demonstrated skills and identified gaps rather than repeating beginner material.

---

## Portfolio Links

- GitHub: https://github.com/prasiddhapal
- TryHackMe: https://tryhackme.com/p/famous33
- LinkedIn: https://linkedin.com/in/prasiddha-pal
- Medium: https://medium.com/@prasiddhapal

---

## Security & Ethics

All investigations are performed in **authorized lab environments** using synthetic, sanitized, or intentionally vulnerable data.

Do not use techniques from this repository against systems, accounts, or networks without explicit authorization.

---

## License

MIT License. Use, fork, and adapt for personal and educational purposes.

---

**Status: 🟢 Active | Day 44 Complete**

> **Investigate the evidence. Correlate the telemetry. Validate the hypothesis. Document the decision.**
