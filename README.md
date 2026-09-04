# SOC Analyst Journey
Practical, evidence-driven labs and investigations to build hands-on SOC, detection engineering, and DFIR skills.

---

## Table of contents
- [Overview](#overview)
- [Learning outcomes](#learning-outcomes)
- [Repository contents](#repository-contents)
- [Investigation workflow](#investigation-workflow)
- [Documentation standard](#documentation-standard)
- [Recommended tools & environment](#recommended-tools--environment)
- [How to use this repository](#how-to-use-this-repository)
- [Contributing](#contributing)
- [License & contact](#license--contact)

---

## Overview
This repository documents a structured, practical learning path for aspiring SOC analysts and detection engineers. It emphasizes reproducible investigations, evidence-first reasoning, and clear documentation so that other analysts can validate and reproduce findings. Content ranges from foundational OS and networking topics to advanced detection engineering, threat hunting, and incident response.

Key goals:
- Teach investigative thinking and workflows used by modern SOC teams
- Provide reproducible labs and real-world style scenarios
- Demonstrate detection engineering and SIEM validation
- Produce clear, shareable investigation artifacts and reports

---

## Learning outcomes
After working through these modules you will be able to:
- Triage alerts and perform structured investigations
- Collect and validate forensic evidence from endpoints and network sources
- Reconstruct timelines and map incidents to MITRE ATT&CK
- Design and validate detection rules and reduce false positives
- Use automation and AI as analyst assistants while retaining human verification

---

## Repository contents
Top-level layout (each module follows the Documentation Standard below):

SOC_Journey/
├── Day-XX-Topic/           # Module folder (one per lab / investigation)
│   ├── README.md           # Module overview & objectives
│   ├── commands.md         # Reproducible commands, queries, and scripts
│   ├── investigation.md    # Chronological investigation notes and reasoning
│   ├── findings.md         # Summary of findings, IOCs, and remediation
│   ├── validation.md       # How results were validated (tests, queries)
│   └── Screenshots/        # Evidence artifacts (images, captures)

Other top-level directories:
- Detection-Engineering/
- Threat-Hunting/
- Incident-Response/
- Malware-Analysis/
- Windows/
- Linux/
- Projects/

---

## Investigation workflow
Every investigation follows the same repeatable workflow to ensure rigor and reproducibility:

1. Alert / hypothesis — why this event is suspicious
2. Evidence collection — what logs, files, or artifacts were gathered
3. Artifact analysis — what the evidence shows
4. Correlation — link related events across sources
5. Validation — confirm findings and eliminate false positives
6. Scope & impact — identify affected systems and accounts
7. Attack mapping — map steps to MITRE ATT&CK techniques
8. Recommendations — containment, remediation, and hardening
9. Documentation — final report with reproducible commands and artifacts

Principles: trust the evidence, prefer reproducible commands/queries, and keep analyst decisions auditable.

---

## Documentation standard
To make every investigation reproducible and reviewable, each module must include:
1. Objective: What was investigated and why
2. Evidence collected: Artifacts and data sources with collection timestamps
3. Reproducible commands & queries: exact commands and SIEM searches
4. Analysis: What the evidence shows and why it matters
5. Validation steps: How you confirmed the finding
6. IOCs: Files, hashes, IPs, domains, registry keys, process hashes, etc.
7. MITRE ATT&CK mapping (where applicable)
8. Recommended response & remediation
9. Lessons learned and open questions

Screenshots are optional supplements; textual evidence and commands are primary.

---

## Recommended tools & environment
Suggested toolset used across the repository:
- OS: Linux, Windows, and Kali for lab work
- Shells & scripting: Bash, Python, PowerShell
- SIEM: Splunk (primary examples), configurable for others
- Network analysis: Wireshark, tcpdump
- Memory forensics: Volatility 3
- Repository & collaboration: Git, GitHub
- Utilities: ss, netstat, dig, curl, ssh, ps, journalctl

Each module lists the exact tooling and versions used for reproducibility.

---

## How to use this repository
- Read module README.md for objectives and prerequisites.
- Reproduce the lab by following commands.md in order (use an isolated lab environment).
- Review investigation.md for analyst reasoning and timeline reconstruction.
- Validate findings with validation.md and any provided test cases.
- Use findings.md for quick reference when building detection rules or running hunts.

If you want an aggregated Table of Contents for all Day-XX modules, I can generate one automatically.

---

## Contributing
Contributions are welcome. To maintain quality and reproducibility, please follow these guidelines:
- Create an issue describing the proposed change or new module before opening a PR.
- Each investigation contribution MUST follow the Documentation Standard section above.
- Include reproducible commands, sample logs or sanitized artifacts, and expected results.
- Add MITRE ATT&CK mappings where applicable.
- Keep sensitive data out of the repo — sanitize IOCs and replace with placeholders when needed.

I can add a CONTRIBUTING.md template that enforces these rules if you want — say the word and I’ll create it.

---

## License & contact
Please add your preferred license and contact details here. If you want, I can add a default license (MIT) and a CONTACT.md with your preferred email or link.

---

If you'd like, I can:
- Commit this updated README to your repository
- Create a CONTRIBUTING.md template that enforces the documentation standard
- Generate a per-module TOC with anchors for every Day-XX folder

Tell me which of the above I should do next and I will proceed.
