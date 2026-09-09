# SOC Analyst Journey

> A structured, hands-on cybersecurity portfolio focused on **SOC operations, SIEM, detection engineering, threat hunting, DFIR, network security, identity security, malware analysis, and cloud security**.

[![Status](https://img.shields.io/badge/Status-Active-brightgreen)](https://github.com/prasiddhapal/SOC_journey)
[![Repository](https://img.shields.io/badge/Portfolio-SOC%20Journey-blue)](https://github.com/prasiddhapal/SOC_journey)
[![Focus](https://img.shields.io/badge/Focus-SOC%20%7C%20Blue%20Team%20%7C%20DFIR-informational)](https://github.com/prasiddhapal/SOC_journey)

## About

This repository documents a practical **SOC Analyst development journey** built around hands-on investigations, security telemetry, incident analysis, detection engineering, and forensic workflows.

The objective is to develop the ability to investigate real-world security scenarios methodically:

```text
Telemetry
   ↓
Evidence
   ↓
Observation
   ↓
Hypothesis
   ↓
Correlation
   ↓
Validation
   ↓
Confidence
   ↓
Conclusion
   ↓
Detection / Response
```

The repository emphasizes **practical investigation and analyst reasoning**, not tool collecting or theoretical memorization.

---

## Core Capabilities

### SOC Operations
- Alert triage
- Security event investigation
- Incident analysis
- Evidence collection
- Timeline reconstruction
- False-positive validation
- Investigation reporting

### SIEM & Detection Engineering
- Splunk / SPL
- IBM QRadar
- Log filtering and correlation
- Authentication hunting
- Baseline and anomaly detection
- Detection logic
- Detection validation and tuning

### Windows & Identity Security
- Windows Security Event Logs
- Sysmon
- PowerShell
- Active Directory
- Kerberos
- NTLM
- Account and group investigation
- Privileged identity analysis

### Network Security
- TCP/IP
- DNS
- HTTP/S
- SMB
- Wireshark
- TShark
- PCAP analysis
- Network reconnaissance
- C2 traffic investigation

### DFIR & Malware Analysis
- Volatility 3
- Memory forensics
- Process investigation
- File and artifact analysis
- JavaScript and browser-extension analysis
- Credential-theft investigation
- Keylogging and exfiltration analysis
- IOC extraction

### Threat Intelligence
- VirusTotal
- MalwareBazaar
- ThreatFox
- Hash, domain, IP, and infrastructure analysis
- MITRE ATT&CK

### Cloud Security
- AWS forensics fundamentals
- CloudTrail fundamentals
- IAM fundamentals
- Cloud identity investigation

---

## Tool & Framework Stack

| Area | Tools / Frameworks |
|---|---|
| SIEM | Splunk, IBM QRadar |
| Network Analysis | Wireshark, TShark, tcpdump |
| Windows Telemetry | Windows Event Logs, Sysmon, PowerShell |
| DFIR | Volatility 3 |
| Threat Intelligence | VirusTotal, MalwareBazaar, ThreatFox |
| Detection | SPL, MITRE ATT&CK |
| Linux Analysis | Bash, grep, awk, sed, journalctl, ps, ss |
| Security Testing | Nmap, Burp Suite, Metasploit, OWASP ZAP |
| Cloud | AWS, CloudTrail fundamentals, IAM fundamentals |
| Version Control | Git, GitHub |

Tools are included because they support **investigation, detection, hunting, response, or interview readiness**. Production experience is not claimed unless it was actually demonstrated hands-on.

---

## Investigation Methodology

Every investigation follows a repeatable analyst workflow:

### 1. Alert or Hypothesis
Define what appears suspicious and why.

### 2. Evidence Collection
Gather the relevant logs, artifacts, network data, or memory evidence.

### 3. Artifact Analysis
Determine what each artifact actually shows.

### 4. Correlation
Connect events across identity, endpoint, network, and SIEM telemetry.

### 5. Validation
Test the hypothesis and eliminate reasonable benign explanations.

### 6. Scope & Impact
Identify affected users, systems, accounts, infrastructure, and potential impact.

### 7. Attack Mapping
Map relevant behavior to MITRE ATT&CK techniques.

### 8. Detection / Response
Develop detection opportunities and identify appropriate containment or remediation actions.

### 9. Documentation
Record evidence, reasoning, confidence, conclusions, and reproducible investigation steps.

### Analyst Standard

The repository intentionally separates:

```text
Evidence
   ↓
Observation
   ↓
Hypothesis
   ↓
Confidence
   ↓
Conclusion
```

This prevents a suspicious indicator from being presented as confirmed compromise without sufficient evidence.

---

## Journey Structure

### Phase I | Linux Security Foundations

**Days 1–19**

Core Linux investigation skills:

- Authentication logs
- SSH
- Brute-force detection
- Users and permissions
- Processes
- Services and system logs
- Networking
- Firewall investigation
- File integrity
- SUID/SGID and special permissions
- Linux capabilities
- IOC hunting
- Process/network correlation
- Authentication and user activity

### Phase II | SOC Operations & SIEM

**Days 20–30**

Practical SOC and SIEM skills:

- Phishing investigation
- Alert triage
- Windows event investigation
- Splunk investigation
- SPL
- Detection engineering
- Transaction analysis
- Authentication hunting
- Context-aware detection
- Alert validation
- Multi-source correlation

### Phase III | DFIR, Threat Intelligence & Enterprise Telemetry

**Days 31–39**

Advanced investigation capabilities:

- Memory forensics
- Volatility 3
- Threat intelligence
- Wireshark / PCAP analysis
- AWS cloud forensics fundamentals
- Windows logging
- Sysmon
- PowerShell
- Linux enterprise logging
- Network traffic analysis
- SIEM log analysis
- HTB Sherlock investigation
- IBM QRadar

### Phase IV | Advanced Investigations & Identity Security

**Days 40+**

The journey expands into:

- Multi-stage DFIR
- Malware analysis
- Browser-extension security
- Covert data exfiltration
- Active Directory
- Kerberos
- NTLM
- Privileged identity investigation
- Identity threat hunting
- Detection engineering
- Endpoint investigation
- Cloud identity security
- Incident response
- SOC capstone investigations

---

## Selected Investigation Highlights

### Multi-Stage DFIR
Reconstructed attack chains through **PCAP, SMB, web shells, reverse shells, memory forensics, persistence, malware analysis, and C2 investigation**.

### SIEM Investigation
Used **Splunk and QRadar** to investigate authentication, process, network, application, and endpoint telemetry.

### Windows Security Monitoring
Analyzed Windows authentication and endpoint telemetry including:

```text
4624
4625
4688
4768
4769
4771
```

along with Sysmon and PowerShell activity.

### Malware Analysis
Investigated malicious browser-extension behavior involving:

```text
Credential Theft
Keylogging
AES Encryption
Base64 Encoding
Covert Exfiltration
Anti-Analysis
```

### Identity Threat Hunting
Used Splunk to baseline Kerberos activity, identify rare service relationships, correlate source information, and validate whether suspicious activity supported a malicious hypothesis.

---

## Documentation Standard

Individual investigations are documented as separate day-level modules.

A module may contain:

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

### Documentation expectations

**README.md**
- Objective
- Scenario
- Prerequisites
- Investigation overview
- Key findings
- Investigation flow

**commands.md**
- Reproducible commands
- SIEM queries
- Query purpose
- Expected output

**investigation.md**
- Chronological investigation
- Evidence
- Analyst reasoning
- Correlation
- Tested assumptions
- Timeline

**findings.md**
- Executive summary
- IOCs
- ATT&CK mapping
- False positives
- Impact
- Response
- Lessons learned

**validation.md**
- Verification steps
- Expected results
- Negative tests
- Detection validation

**Screenshots/**
- Meaningful evidence from the investigation
- Query output
- Terminal output
- Forensic artifacts
- Relevant investigation results

Completion screenshots alone are not treated as evidence of analytical work.

---

## Portfolio & Interview Focus

The journey is designed to develop both **technical capability and analyst communication**.

For each investigation, the goal is to explain:

```text
What happened?
How do you know?
What evidence supports it?
What did you correlate?
What did you rule out?
How confident are you?
What would you do next?
```

This mirrors the reasoning expected in SOC analyst interviews and real incident investigations.

---

## Learning Roadmap

The roadmap evolves as skills are demonstrated.

```text
Linux Security
      ↓
Networking
      ↓
Windows & Authentication
      ↓
SOC Triage
      ↓
SIEM
      ↓
Splunk
      ↓
Detection Engineering
      ↓
Windows Logging / Sysmon
      ↓
Network Analysis
      ↓
Threat Intelligence
      ↓
Memory Forensics
      ↓
Cloud Forensics
      ↓
Active Directory / Identity
      ↓
Threat Hunting
      ↓
Endpoint Detection
      ↓
Cloud Identity
      ↓
Incident Response
      ↓
SOC Capstone
      ↓
Job-Ready Assessment
```

The next phase prioritizes areas that provide the highest value for a modern SOC analyst:

- Active Directory and identity security
- Endpoint investigation
- Detection engineering
- Threat hunting
- Cloud identity and cloud forensics
- Incident response
- Multi-source SOC capstones

---

## Security & Ethics

All investigations in this repository are performed in **authorized lab environments** using synthetic, sanitized, or intentionally vulnerable data.

Security testing techniques must only be used against systems for which explicit authorization has been provided.

---

## Repository Navigation

Start with a day-level module:

```bash
git clone https://github.com/prasiddhapal/SOC_journey.git
cd SOC_journey
```

Then open the investigation folder of interest and begin with its `README.md`.

The repository is intended to work both as:

- a personal SOC Analyst training record
- a public cybersecurity portfolio
- an interview preparation reference
- a collection of reproducible investigation workflows

---

## Portfolio

- **GitHub:** https://github.com/prasiddhapal
- **TryHackMe:** https://tryhackme.com/p/famous33
- **LinkedIn:** https://linkedin.com/in/prasiddha-pal
- **Medium:** https://medium.com/@prasiddhapal

---

## License

MIT License. Use, fork, and adapt for personal and educational purposes.

---

> **Investigate the evidence. Correlate the telemetry. Validate the hypothesis. Document the decision.**
