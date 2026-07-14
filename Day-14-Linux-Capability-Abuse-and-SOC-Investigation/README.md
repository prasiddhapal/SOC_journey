# Linux Capability Abuse Detection and SOC Investigation

## 📖 Introduction

Linux Capabilities provide applications with only the privileges they require, following the Principle of Least Privilege. While they improve security compared to SUID, attackers may abuse capabilities to gain elevated privileges. This lab focused on identifying Linux capabilities, investigating running processes, and applying a structured SOC investigation workflow.

---

## 🎯 Learning Objectives

- Understand the difference between file and process capabilities.
- Learn the purpose of `getpcaps`.
- Detect potential capability abuse.
- Investigate privilege escalation attempts.
- Follow an evidence-based SOC investigation workflow.

---

## 📚 Topics Covered

### Linux Capabilities

- getpcaps
- File vs Process Capabilities
- Capability Abuse
- Privilege Escalation

### SOC Investigation

- Process Analysis
- Parent Process Analysis
- Capability Verification
- Network Investigation
- Evidence Collection
- Incident Escalation

---

## 🛡️ Practical Activities

- Verified `getpcaps` installation.
- Investigated running process capabilities.
- Compared `getcap` and `getpcaps`.
- Analyzed capability abuse scenarios.
- Performed a complete SOC investigation exercise.

---

## 📂 Documentation

- Commands → commands.md
- Notes → notes.md
- Interview Questions → interview_questions.md

---

## 🎯 Key Takeaways

- `getcap` checks file capabilities.
- `getpcaps` checks capabilities of running processes.
- Capability abuse can be used for privilege escalation.
- Always verify, collect evidence, analyze, document, and escalate before taking action.
