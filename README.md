# 🛡️ SOC Analyst Journey

> A hands-on cybersecurity portfolio focused on building practical **Blue Team, SOC investigation, detection engineering, and DFIR skills** through structured labs, real investigation scenarios, evidence-based analysis, and professional documentation.

![Status](https://img.shields.io/badge/Status-Active%20Learning-brightgreen)
![Focus](https://img.shields.io/badge/Focus-SOC%20%7C%20Blue%20Team-blue)
![Approach](https://img.shields.io/badge/Approach-Hands--On-orange)
![Documentation](https://img.shields.io/badge/Documentation-GitHub-lightgrey)

---

## 🎯 Purpose

This repository documents a practical journey toward becoming a capable **SOC Analyst**.

The focus is not on collecting commands or completing isolated tutorials. Each topic is reinforced through:

- Hands-on labs
- Security investigations
- Detection logic
- Evidence collection
- Log and process analysis
- Threat hunting
- Incident-response thinking
- MITRE ATT&CK mapping
- Screenshots and reproducible evidence
- Technical documentation
- Interview-oriented explanations

The goal is to understand **how and why an analyst investigates an alert**, not simply how to run a tool.

---

## 🧭 Learning Path

The journey progresses from foundational system knowledge into operational security work:

```text
Linux & System Fundamentals
          │
          ▼
Networking & Security Fundamentals
          │
          ▼
Windows & Endpoint Analysis
          │
          ▼
Logs & Authentication Investigation
          │
          ▼
SIEM Investigation
          │
          ▼
Detection Engineering
          │
          ▼
Threat Hunting
          │
          ▼
Incident Response & DFIR
          │
          ▼
Practical Security Challenges
          │
          ▼
Automation & AI-Assisted SOC Workflows
```

This structure is intentionally iterative. Earlier fundamentals are repeatedly applied during later investigations.

---

## 🔐 Core Areas

### 🐧 Linux & System Security

- Linux administration
- File systems and permissions
- Users and groups
- Processes and services
- Authentication
- System and security logs
- Networking utilities
- Firewall fundamentals
- Bash-based analysis and automation

### 🌐 Networking

- TCP/IP fundamentals
- DNS
- DHCP
- Routing
- Ports and sockets
- SSH
- HTTP/HTTPS
- Network troubleshooting
- Packet and traffic analysis

### 🪟 Windows & Endpoint Security

- Windows process analysis
- PowerShell investigation
- Process trees and parent-child relationships
- Windows command-line analysis
- Endpoint artifacts
- Authentication and account context
- Memory forensics
- Suspicious execution analysis

### 📊 SIEM & Log Investigation

- Splunk investigations
- Authentication analysis
- Event correlation
- Timeline analysis
- Suspicious process detection
- Context enrichment
- Risk scoring
- Analyst decision logic
- Evidence-based alert triage

### 🎯 Detection Engineering

- Detection logic
- Suspicious behavior identification
- IOC-based detection
- Context-aware detection
- Correlation rules
- Risk scoring
- Detection validation
- False-positive consideration
- MITRE ATT&CK alignment

### 🔎 Threat Hunting

- Hypothesis-driven hunting
- IOC hunting
- Process and command-line analysis
- Authentication hunting
- Timeline reconstruction
- Cross-event correlation
- Endpoint and network context

### 🚨 Incident Response & DFIR

- Alert triage
- Evidence preservation
- Scope assessment
- Root-cause investigation
- Endpoint investigation
- Memory forensics
- IOC extraction
- Attack-chain reconstruction
- Containment recommendations
- Investigation reporting

---

## 🧪 Practical Investigation Approach

Investigations are structured around a repeatable analyst workflow:

```text
Alert / Hypothesis
        │
        ▼
Collect Evidence
        │
        ▼
Analyze Artifacts
        │
        ▼
Correlate Events
        │
        ▼
Validate the Finding
        │
        ▼
Determine Scope & Impact
        │
        ▼
Map the Attack
        │
        ▼
Recommend Response
        │
        ▼
Document Evidence & Lessons
```

### Investigation Principle

> **Trust the evidence. Validate the finding. Question the assumption.**

A suspicious indicator is treated as a starting point, not a conclusion.

---

## 🛠️ Security Toolkit

| Area | Tools / Technologies |
|---|---|
| Operating Systems | Linux, Kali Linux, Windows |
| Shell & Scripting | Bash, Python, PowerShell |
| SIEM | Splunk |
| Network Analysis | Wireshark, tcpdump |
| Memory Forensics | Volatility 3 |
| Security Frameworks | MITRE ATT&CK |
| Version Control | Git, GitHub |
| Networking | ss, netstat, dig, curl, SSH |
| System Analysis | ps, journalctl, Windows process tools |
| Practice Platforms | CyberDefenders and other hands-on labs |

Tools are introduced when they solve an investigation problem, rather than being treated as isolated technologies.

---

## 📁 Repository Organization

The repository combines structured learning modules with practical investigation work.

```text
SOC_Journey/
│
├── Day-XX-Topic/
│   ├── README.md
│   ├── commands.md
│   ├── findings.md
│   ├── investigation.md
│   ├── validation.md
│   └── Screenshots/
│
├── Detection-Engineering/
├── Threat-Hunting/
├── Incident-Response/
├── Malware-Analysis/
├── Windows/
├── Linux/
└── Projects/
```

Individual modules may contain different documentation files depending on the investigation.

---

## 📝 Documentation Standard

Practical work is documented so that another analyst can understand:

1. **What was investigated**
2. **Why it was investigated**
3. **Which evidence was collected**
4. **Which commands or queries were used**
5. **What the evidence showed**
6. **How the finding was validated**
7. **What indicators were identified**
8. **How the activity maps to security concepts**
9. **What response actions are appropriate**
10. **What was learned**

Screenshots are used as supporting evidence, not as a substitute for analysis.

---

## 🔬 Investigation Examples

The repository includes practical work covering areas such as:

- Authentication and login investigations
- Suspicious process analysis
- PowerShell detection
- Context-aware Splunk detection
- Risk scoring and alert triage
- Event correlation and timeline analysis
- Network and IOC investigation
- Memory forensics
- Malware execution analysis
- MITRE ATT&CK technique identification
- End-to-end incident investigation

---

## 🧠 From Detection to Investigation

A major focus of this journey is moving beyond simple alert creation.

```text
Detect
  ↓
Understand Context
  ↓
Correlate Evidence
  ↓
Investigate
  ↓
Validate
  ↓
Assess Risk
  ↓
Respond
  ↓
Document
```

For example, a suspicious PowerShell event becomes more useful when combined with:

- Parent process
- User identity
- Source IP
- Command line
- Event timing
- Related processes
- Network activity
- Risk score
- Historical context

This is the difference between **finding an event** and **investigating an incident**.

---

## 🤖 AI-Assisted SOC Workflows

AI is treated as an analytical assistant, not an authority.

```text
Security Data
     ↓
AI-Assisted Analysis
     ↓
Human Verification
     ↓
Evidence Validation
     ↓
Analyst Decision
     ↓
Documented Finding
```

The principle is simple:

> **AI can accelerate analysis, but evidence makes the decision.**

AI-assisted work is used for investigation support, documentation, correlation ideas, and workflow improvement while maintaining human validation.

---

## 📈 What This Repository Demonstrates

This portfolio is designed to demonstrate practical capability in:

- Security monitoring
- Alert investigation
- Log analysis
- Endpoint investigation
- SIEM usage
- Detection engineering
- Threat hunting
- Incident response
- Digital forensics
- Evidence-based reasoning
- Technical documentation

The repository is continuously refined as new investigations add deeper technical context.

---

## 🏁 Professional Objective

The long-term objective is to develop the practical skills and investigative mindset required for a modern **SOC / Blue Team role**.

That means being able to:

- Investigate alerts independently
- Understand endpoint and network evidence
- Build and validate detections
- Hunt for related activity
- Reconstruct attack timelines
- Communicate findings clearly
- Recommend appropriate response actions
- Document investigations professionally

---

## 📚 Learning Philosophy

Cybersecurity is learned through **practice, investigation, repetition, and validation**.

The emphasis throughout this repository is:

---

## ⭐ Closing Principle

> **Detect the signal. Understand the context. Validate the evidence. Investigate the story. Document the conclusion.**

This repository is a living record of that process.
