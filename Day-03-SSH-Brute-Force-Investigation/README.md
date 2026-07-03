# 🛡️ Day 03 – SSH Brute Force Investigation

> **Case ID:** SOC-DAY03-001

## 📌 Overview

This investigation demonstrates how to generate and analyze failed SSH authentication events in a controlled Kali Linux lab. The objective was to understand how Linux records authentication failures, identify brute-force indicators, and perform an evidence-based security investigation.

---

## 🎯 Objectives

- Generate failed SSH authentication events.
- Analyze SSH authentication logs.
- Identify invalid user attempts.
- Understand brute-force indicators.
- Perform evidence-based log analysis.
- Document the investigation professionally.

---

## 🧪 Lab Environment

| Component | Details |
|----------|---------|
| Operating System | Kali Linux |
| Service | OpenSSH Server (`sshd`) |
| Log File | `/var/log/auth.log` |
| Investigation Type | SSH Authentication Analysis |

---

## 🛠 Tools Used

- OpenSSH Server
- systemctl
- SSH Client
- grep
- Kali Linux Terminal

---

## 📂 Project Structure

```text
Day-03-SSH-Brute-Force-Investigation
│
├── README.md
├── Notes
│   ├── 01-Failed-SSH-Authentication.md
│   ├── 02-Invalid-User-Attempts.md
│   ├── 03-Brute-Force-Indicators.md
│   ├── 04-SSH-Log-Analysis.md
│   ├── 05-Commands-Reference.md
│   ├── 06-Event-Timeline.md
│   ├── 07-Investigation-Conclusion.md
│   └── 08-Learning-Notes.md
│
├── screenshots
└── resources
```

---

## 📖 Investigation Workflow

1. Verified the SSH service.
2. Generated failed SSH authentication attempts.
3. Collected authentication logs.
4. Analyzed SSH log entries.
5. Reconstructed the event timeline.
6. Performed an evidence-based investigation.
7. Documented findings and conclusions.

---

## 🔍 Key Findings

- Failed SSH authentication events were successfully generated.
- The username **wronguser** was identified as a non-existent account.
- Authentication logs recorded `Invalid user` and `Failed password` events.
- The activity originated from **127.0.0.1 (Loopback Address)**.
- No evidence of a successful compromise was observed.

---

## 📌 Investigation Outcome

**Severity:** 🟢 Low

**Final Verdict:**

The observed authentication events were generated intentionally within a controlled laboratory environment and were classified as **False Positive (Expected Lab Activity)**.

---

## 📚 Skills Demonstrated

- Linux Authentication Log Analysis
- SSH Authentication Investigation
- Authentication Failure Analysis
- Log Correlation
- Event Timeline Reconstruction
- Incident Documentation
- Basic SOC Investigation

---

## 🚀 Author

**Prasiddha Pal**

SOC Analyst Trainee

---

⭐ **Part of the SOC Journey – Building Practical SOC Investigation Skills**
