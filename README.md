# 🛡️ SOC Analyst Journey

A hands-on cybersecurity portfolio focused on building practical Blue Team, SOC investigation, detection engineering, and DFIR skills through structured labs and reproducible investigations.

---

## Table of contents
- [Purpose](#purpose)
- [Learning path](#learning-path)
- [Core areas](#core-areas)
- [Practical investigation approach](#practical-investigation-approach)
- [Security toolkit](#security-toolkit)
- [Repository organization](#repository-organization)
- [Documentation standard](#documentation-standard)
- [Investigation examples](#investigation-examples)
- [From detection to investigation](#from-detection-to-investigation)
- [AI-assisted SOC workflows](#ai-assisted-soc-workflows)
- [What this repository demonstrates](#what-this-repository-demonstrates)
- [Professional objective](#professional-objective)
- [How to use / contribute](#how-to-use--contribute)

---

## Purpose
This repository documents a practical, evidence-driven journey toward becoming a capable SOC Analyst. The emphasis is on investigations and reasoning — not just cataloging commands. Each module contains:
- Hands-on labs
- Real investigation scenarios with reproducible evidence
- Detection logic and validation
- Timeline reconstruction and reporting
- MITRE ATT&CK mapping where applicable

The goal is to show how and why an analyst investigates an alert, not merely how to run tools.

## Learning path
Progression used throughout the repository (early topics feed into later, more applied work):
1. Linux & system fundamentals
2. Networking & security fundamentals
3. Windows & endpoint analysis
4. Logs & authentication investigation
5. SIEM investigation
6. Detection engineering
7. Threat hunting
8. Incident response & DFIR
9. Practical security challenges
10. Automation & AI-assisted SOC workflows

## Core areas
### Linux & system security
- Administration, filesystems, permissions, users/groups
- Processes, services, authentication, system logs, Bash automation

### Networking
- TCP/IP, DNS, DHCP, routing, ports/sockets
- SSH, HTTP/HTTPS, packet & traffic analysis

### Windows & endpoint security
- Process analysis, PowerShell investigation, process trees
- Endpoint artifacts, memory forensics, suspicious execution

### SIEM & log investigation
- Splunk investigations, event correlation, timeline analysis
- Authentication analysis, context enrichment, risk scoring

### Detection engineering
- Detection logic, IOC-based & context-aware detection
- Correlation rules, validation, false-positive handling

### Threat hunting
- Hypothesis-driven hunting, IOC hunting, cross-event correlation

### Incident response & DFIR
- Triage, evidence preservation, scope assessment, root-cause analysis

## Practical investigation approach
A repeatable analyst workflow used across modules:
1. Alert / Hypothesis
2. Collect evidence
3. Analyze artifacts
4. Correlate events
5. Validate the finding
6. Determine scope & impact
7. Map the attack
8. Recommend response
9. Document evidence & lessons

Principles: trust the evidence, validate findings, and treat indicators as starting points.

## Security toolkit
- Operating systems: Linux, Kali, Windows
- Shell & scripting: Bash, Python, PowerShell
- SIEM: Splunk (primary examples)
- Network analysis: Wireshark, tcpdump
- Memory forensics: Volatility 3
- Frameworks: MITRE ATT&CK
- Version control: Git, GitHub
- Common utilities: ss, netstat, dig, curl, ssh, ps, journalctl

Tools are introduced to solve investigation problems — not as isolated topics.

## Repository organization
Top-level layout (each module follows the documentation standard):

SOC_Journey/
├── Day-XX-Topic/
│   ├── README.md          # high-level overview of the module
│   ├── commands.md        # commands and queries used
│   ├── findings.md        # concise findings and IOCs
│   ├── investigation.md   # step-by-step investigation notes
│   ├── validation.md      # how findings were validated
│   └── Screenshots/       # evidence (screenshots, images)

Other top-level folders:
- Detection-Engineering/
- Threat-Hunting/
- Incident-Response/
- Malware-Analysis/
- Windows/
- Linux/
- Projects/

Individual modules may contain additional files depending on the investigation.

## Documentation standard
Every investigation should make it possible for another analyst to reproduce and understand the work. Include:
1. What was investigated
2. Why it was investigated
3. Which evidence was collected
4. Exact commands or queries used (with context)
5. What the evidence showed
6. How the finding was validated
7. Indicators of compromise (IOCs) discovered
8. Mapping to MITRE ATT&CK techniques where applicable
9. Recommended response actions
10. Lessons learned

Screenshots support analysis but are not a substitute for textual evidence and commands.

## Investigation examples
Modules cover practical scenarios such as:
- Authentication and login investigations
- Suspicious process and PowerShell analysis
- Context-aware Splunk detection and correlation
- Risk scoring and alert triage
- Memory forensics and malware execution analysis
- End-to-end incident investigations with timelines

## From detection to investigation
Detect → Understand context → Correlate evidence → Investigate → Validate → Assess risk → Respond → Document

A single alert becomes valuable only after enrichment with parent process, user identity, source IP, command line, timing, related processes, and historical context.

## AI-assisted SOC workflows
AI is an assistant, not an authority. Typical flow:
- Security data → AI-assisted analysis → Human verification → Evidence validation → Analyst decision → Documented finding

Use AI to accelerate analysis, suggest correlations, and draft documentation — always verify with evidence.

## What this repository demonstrates
Practical capability in: security monitoring, alert investigation, log analysis, endpoint investigation, detection engineering, threat hunting, incident response, and digital forensics.

## Professional objective
Develop the investigative mindset and practical skills required for modern SOC / Blue Team roles: independent investigations, detection validation, attack reconstruction, clear communication, and professional reporting.

## How to use & contribute
- Browse Day-XX modules to follow the learning path.
- Use commands.md and investigation.md to reproduce analyses.
- Open issues or pull requests with improvements, new investigations, or corrections.
- When contributing investigations, follow the documentation standard above.

---

If you want, I can further:
- Add a TOC with line anchors for each Day-XX module automatically
- Create a CONTRIBUTING.md template that enforces the documentation standard
- Split very long sections into separate markdown files under docs/

License / contact: add your preferred license or contact details at the end of this file.
