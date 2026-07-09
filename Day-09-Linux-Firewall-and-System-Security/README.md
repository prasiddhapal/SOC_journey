# Linux Firewall and System Security for SOC Analysts

## 📖 Introduction

Firewalls are one of the first layers of defense in a secure environment. A SOC analyst should understand how firewall rules control network traffic, protect services, and support incident investigations. This lab focuses on managing Linux firewall rules using UFW and applying firewall concepts during security investigations.

---

## 🎯 Learning Objectives

- Understand the role of a firewall
- Differentiate between Host-Based and Network Firewalls
- Manage firewall rules using UFW
- Analyze firewall configurations
- Understand common network service ports
- Apply firewall concepts in SOC investigations

---

## 📚 Topics Covered

### Firewall Fundamentals

- Firewall
- Host-Based Firewall
- Network Firewall

### UFW

- Status
- Verbose Mode
- Numbered Rules
- Application Profiles
- Allow Rules
- Deny Rules
- Reload
- Reset

### Common Service Ports

- SSH (22)
- Telnet (23)
- DNS (53)
- HTTP (80)
- HTTPS (443)
- RDP (3389)

### Security Concepts

- Defense in Depth
- Firewall Rule Investigation

---

## 🛡️ Practical Investigation

During this lab the following investigations were performed:

- Verified firewall status and default policies.
- Examined configured firewall rules.
- Investigated OpenSSH application profile.
- Allowed and denied firewall rules.
- Reviewed common service ports.
- Applied firewall concepts to SOC investigation scenarios.

---

## 📂 Documentation

- Commands → commands.md
- Notes → notes.md
- Interview Questions → interview_questions.md

---

## 📸 Screenshots

- Firewall Status Analysis
- Firewall Rule Analysis
- OpenSSH Profile Analysis

---

## 🎯 Key Takeaways

- Firewalls control incoming and outgoing network traffic using predefined rules.
- Host-based and network firewalls provide different layers of protection.
- Firewall rules should never be modified without proper investigation.
- Firewall events should always be correlated with processes, logs, and network activity before taking action.
