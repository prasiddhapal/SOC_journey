# 🔍 SOC Analyst Journey

Practical, hands-on labs and real-world investigations to build **SOC analysis**, **detection engineering**, and **DFIR** skills through evidence-driven methodology.

**Status:** 🟢 Active | **Modules:** 39+ | **Created:** July 2026

---

## ⚡ Quick Start

```bash
# Clone the repository
git clone https://github.com/prasiddhapal/SOC_journey.git
cd SOC_journey

# Pick a module (e.g., Day-01)
cd Day-01-Linux-Authentication-Logs

# Follow the investigation workflow
# 1. Read README.md for objectives
# 2. Run commands.md (commands & queries in order)
# 3. Review investigation.md (analyst reasoning)
# 4. Check findings.md (IOCs & recommendations)
# 5. Validate with validation.md (test cases & expected results)
```

---

## 📚 Table of Contents

- [What You'll Learn](#what-youll-learn)
- [Module Index](#module-index)
- [Investigation Workflow](#investigation-workflow)
- [Documentation Standard](#documentation-standard)
- [Recommended Tools](#recommended-tools)
- [How to Use](#how-to-use)
- [Contributing](#contributing)
- [License & Contact](#license--contact)

---

## 🎯 What You'll Learn

After completing modules in this journey, you will be able to:

- ✅ **Triage & investigate** alerts with structured reasoning
- ✅ **Collect & validate** forensic evidence from endpoints and network logs
- ✅ **Reconstruct timelines** and correlate events across multiple sources
- ✅ **Map attacks** to MITRE ATT&CK techniques
- ✅ **Design & validate** detection rules with minimal false positives
- ✅ **Use automation & AI** as analyst assistants while retaining human judgment
- ✅ **Document findings** for incident response and threat hunting
- ✅ **Prepare** for SOC analyst and detection engineer interviews

---

## 📖 Module Index

### Linux Fundamentals (Days 1–19)
Foundation in Linux investigation techniques for SOC analysts.

| Day | Title | Focus |
|-----|-------|-------|
| 01 | Linux Authentication Logs | auth, wtmp, utmp, lastlog analysis |
| 02 | SSH Authentication Investigation | SSH key analysis, successful logins |
| 03 | SSH Brute-Force Investigation | Failed login patterns, threat detection |
| 04 | Linux Users & Permissions | User management, permission abuse detection |
| 05 | Process Management | Process lifecycle, running processes analysis |
| 06 | Linux Services & Logs | systemd, journalctl, service behavior |
| 07 | Linux Networking for SOC Analysts | Network concepts for security investigations |
| 08 | Linux Network Analysis | Active connections, listening ports, traffic |
| 09 | Linux Firewall & System Security | iptables, ufw, firewall rule investigation |
| 10 | Linux File Investigation & Integrity | File metadata, checksums, hash validation |
| 11 | Linux Archive & Compression | Extracting and analyzing archives |
| 12 | Linux Special Permissions & Ownership | SUID, SGID, sticky bits, privilege analysis |
| 13 | Linux Capabilities & Privilege Escalation | Capability analysis, elevation detection |
| 14 | Linux Capability Abuse & SOC Investigation | Real-world capability abuse scenarios |
| 15 | Linux Log Hunting & IOC Correlation | Cross-source correlation, threat hunting |
| 16 | Linux Logging & Investigation | Comprehensive logging mechanisms |
| 17 | Advanced Linux Commands | grep, awk, sed, find for investigations |
| 18 | Linux Process & Network Investigation | Combined process/network analysis |
| 19 | Linux Authentication & User Activity | User behavior and access patterns |

### SOC & SIEM Operations (Days 20–30)
Alert triage, phishing, and SIEM-based detection.

| Day | Title | Focus |
|-----|-------|-------|
| 20 | SOC Phishing Investigation | Email analysis, URL extraction, IOC hunting |
| 21 | SOC Alert Triage & Network Investigation | Alert validation, correlation, response |
| 22 | Windows Event Investigation | Event Viewer, Windows logs, event correlation |
| 23 | Splunk Investigation | Splunk queries, search anatomy, data enrichment |
| 24 | Splunk Detection | Rule development, thresholding, tuning |
| 25 | Splunk Transaction Analysis | Transaction commands, session analysis |
| 26 | Splunk Authentication Hunting | Login behavior, brute-force detection |
| 27 | Splunk Detection Engineering | Building robust, low-FP detection rules |
| 28 | Splunk Context-Aware Detection | Baseline & anomaly detection techniques |
| 29 | Splunk Alert Triage | Alert validation, response automation |
| 30 | Splunk Correlation Investigations | Multi-source event correlation |

### Advanced Topics (Days 31–39)
Memory forensics, network analysis, cloud security, and SIEM platforms.

| Day | Title | Focus |
|-----|-------|-------|
| 31 | Memory Forensics (Volatility) | Memory dump analysis, process recovery |
| 32 | Threat Intelligence & Wireshark | PCAP analysis, network indicators |
| 33 | AWS Cloud Forensics & Phishing | Cloud log analysis, phishing in AWS |
| 34 | Windows Logging, Sysmon & PowerShell | Advanced Windows logging, script analysis |
| 35 | Linux Logging & SOC | Enterprise Linux logging for SOC teams |
| 36 | Network Traffic Analysis | Protocol analysis, flow-based investigation |
| 37 | SIEM Log Analysis | General SIEM investigation techniques |
| 38 | Brutus Professional | [Placeholder – check module for details] |
| 39 | QRadar 101 | QRadar SIEM basics and workflows |

---

## 🔄 Investigation Workflow

Every investigation follows a **consistent, repeatable methodology** to ensure rigor and auditability:

```
1️⃣  Alert / Hypothesis     → Why is this event suspicious?
2️⃣  Evidence Collection    → What logs/artifacts were gathered?
3️⃣  Artifact Analysis      → What does the evidence show?
4️⃣  Correlation           → Link related events across sources
5️⃣  Validation            → Confirm findings, eliminate false positives
6️⃣  Scope & Impact        → Identify affected systems and accounts
7️⃣  Attack Mapping        → Map to MITRE ATT&CK techniques
8️⃣  Recommendations       → Containment, remediation, hardening
9️⃣  Documentation         → Final report with reproducible commands
```

**Core Principles:**
- 🔐 **Trust the evidence** — Let data drive conclusions
- 🔁 **Reproducibility first** — Every command, query, and finding can be verified
- 📋 **Auditability** — Analyst decisions are documented and transparent
- 🎯 **Clear reasoning** — Investigation steps connect to findings

---

## 📋 Documentation Standard

Every module **must** include these sections to ensure consistency, reproducibility, and quality:

### Required Files

```
Day-XX-Topic/
├── README.md              # Module objectives, prerequisites, overview
├── commands.md            # Exact, reproducible commands & SIEM queries
├── investigation.md       # Chronological reasoning, analyst notes, timeline
├── findings.md            # Summary: IOCs, MITRE ATT&CK mapping, response
├── validation.md          # Test cases, expected outputs, verification steps
└── Screenshots/           # Evidence artifacts (images, log captures)
```

### README.md Checklist
- [ ] Objective: What was investigated and why?
- [ ] Scenario or alert description
- [ ] Prerequisites (tools, access, baseline knowledge)
- [ ] Key findings at a glance
- [ ] Evidence chain or investigation flow diagram

### commands.md Checklist
- [ ] Complete, runnable command sequences
- [ ] SIEM queries with syntax highlighted
- [ ] Expected output for each command
- [ ] Assume isolated lab environment
- [ ] Include comments explaining what each command does

### investigation.md Checklist
- [ ] Timeline reconstruction with timestamps
- [ ] Analyst reasoning for each step
- [ ] What was observed and why it matters
- [ ] Dead ends and assumptions tested
- [ ] Connected events across sources

### findings.md Checklist
- [ ] Executive summary of findings
- [ ] IOCs (files, hashes, IPs, domains, registry keys, process names)
- [ ] MITRE ATT&CK techniques (tactic + technique ID)
- [ ] False positives ruled out
- [ ] Recommended response and remediation
- [ ] Lessons learned

### validation.md Checklist
- [ ] How to verify findings independently
- [ ] Test cases or queries to confirm
- [ ] Expected results and thresholds
- [ ] Negative tests (what should NOT be observed)
- [ ] Links to supporting documentation

---

## 🛠️ Recommended Tools & Environment

### Operating Systems
- **Linux** (primary for investigations)
- **Windows** (for Windows event and PowerShell analysis)
- **Kali Linux** (pre-built toolkit for lab work)

### Core Tools

| Category | Tools | Notes |
|----------|-------|-------|
| **Shells & Scripting** | Bash, Python, PowerShell | Automation and analysis |
| **SIEM** | Splunk, QRadar | Query-based investigations |
| **Network Analysis** | Wireshark, tcpdump, tshark | PCAP analysis, live capture |
| **Memory Forensics** | Volatility 3, MemoryDump | Process & kernel analysis |
| **Log Analysis** | grep, awk, sed, jq | Text processing and parsing |
| **System Tools** | ss, netstat, lsof, ps, journalctl | Process & network inspection |
| **File Analysis** | md5sum, sha256sum, file, strings | Hash validation, metadata |
| **Version Control** | Git, GitHub | Collaboration and tracking |

### Lab Environment Setup
- Isolated, non-production network
- Authorized lab accounts only
- Disposable VMs for each investigation
- Sanitized or synthetic datasets
- Ready-to-use SIEM with sample logs

---

## 🚀 How to Use This Repository

### For Beginners
1. Start with **Day-01** (Linux fundamentals)
2. Follow modules sequentially for building blocks
3. Use **commands.md** to reproduce step-by-step
4. Review **investigation.md** to understand analyst thinking
5. Validate with **validation.md** before moving on

### For SOC Analysts
1. Pick a topic relevant to your current role
2. Read the **README.md** to confirm you have prerequisites
3. Run through **commands.md** in an isolated lab
4. Compare your findings to **findings.md**
5. Adapt techniques to your SIEM platform

### For Detection Engineers
1. Review **Day-23–30** (Splunk detection modules)
2. Study rule development patterns in **commands.md**
3. Use **validation.md** to understand FP testing
4. Adapt queries to your environment (QRadar, ELK, etc.)

### For Interview Prep
1. Review the **findings.md** of 3–5 modules
2. Walk through the investigation workflow on a module
3. Be ready to explain your reasoning for each step
4. Practice answering: "What would you do next?"

---

## 🤝 Contributing

Contributions are welcome! To maintain quality and reproducibility, please follow these guidelines:

### Before You Start
- Create an [issue](https://github.com/prasiddhapal/SOC_journey/issues) describing your proposed module or change
- Describe the investigation scenario, tools used, and learning outcomes
- Ensure the module aligns with the Documentation Standard (see above)

### Submission Checklist
- [ ] Follow the **Documentation Standard** (all 5 required files)
- [ ] Include **reproducible commands** with expected outputs
- [ ] Provide **sample logs or sanitized artifacts**
- [ ] Add **MITRE ATT&CK mapping** (where applicable)
- [ ] Include **expected validation results**
- [ ] Keep **sensitive data out** — use placeholders for real IOCs
- [ ] Write **clear, auditable reasoning** in investigation.md

### Creating a New Module

```bash
# Create a new directory
mkdir Day-XX-Topic-Name

# Create required files
touch Day-XX-Topic-Name/{README.md,commands.md,investigation.md,findings.md,validation.md}
mkdir Day-XX-Topic-Name/Screenshots

# Populate each file following the Documentation Standard
```

---

## 📄 License & Contact

**License:** MIT License — Feel free to use, fork, and adapt for personal and educational use.

**Contact:** [GitHub Issues](https://github.com/prasiddhapal/SOC_journey/issues) — Questions, suggestions, or corrections? Open an issue.

**Author:** [prasiddhapal](https://github.com/prasiddhapal)

---

## 🗺️ Learning Path Roadmap

```
Beginner
  ├─ Day 01–07: Linux basics (auth, SSH, users, processes)
  ├─ Day 08–10: Network & file analysis
  └─ Day 11–14: Permissions & capabilities

Intermediate
  ├─ Day 15–19: Advanced log hunting & correlation
  ├─ Day 20–22: Phishing, alert triage, Windows logs
  └─ Day 23–26: SIEM fundamentals (Splunk queries)

Advanced
  ├─ Day 27–30: Detection engineering & correlation
  ├─ Day 31–33: Memory forensics, network analysis, cloud
  └─ Day 34–39: Enterprise logging, QRadar, advanced tools
```

---

## 📞 Support & Feedback

Have a question or found an issue?

- 🐛 **Bug report:** [Open an issue](https://github.com/prasiddhapal/SOC_journey/issues/new)
- 💡 **Suggestion:** [Discussions](https://github.com/prasiddhapal/SOC_journey/discussions)
- 🔗 **Fork & contribute:** [See Contributing above](#-contributing)

---

**Happy investigating! 🔍**
