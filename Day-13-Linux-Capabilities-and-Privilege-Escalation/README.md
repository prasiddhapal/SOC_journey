# Linux Capabilities and Privilege Escalation for SOC Analysts

## 📖 Introduction

Linux Capabilities provide fine-grained privileges to applications without granting full root access. They follow the Principle of Least Privilege, reducing security risks while allowing programs to perform specific privileged operations. Understanding capabilities is important for SOC analysts investigating privilege escalation and suspicious system behavior.

---

## 🎯 Learning Objectives

- Understand Linux Capabilities.
- Learn the Principle of Least Privilege.
- Identify capabilities using `getcap`.
- Understand how `setcap` assigns or removes capabilities.
- Investigate capability-related security risks from a SOC perspective.

---

## 📚 Topics Covered

### Linux Capabilities

- Principle of Least Privilege
- Linux Capabilities
- getcap
- setcap

### SOC Investigation

- Capability analysis
- Privilege escalation basics
- Evidence collection
- Investigation workflow

---

## 🛡️ Practical Activities

- Verified `getcap` installation
- Enumerated Linux capabilities
- Analyzed common capabilities
- Compared SUID with Linux Capabilities
- Practiced capability investigation workflow

---

## 📂 Documentation

- Commands → commands.md
- Notes → notes.md
- Interview Questions → interview_questions.md

---

## 📸 Screenshots

- Getcap Installation
- Linux Capability Analysis

---

## 🎯 Key Takeaways

- Linux Capabilities provide only the privileges an application requires.
- Capabilities reduce the risks associated with SUID binaries.
- Always investigate unexpected capabilities before making changes.
- Follow an evidence-based investigation process before escalation.
