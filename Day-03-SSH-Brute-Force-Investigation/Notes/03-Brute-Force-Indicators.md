# 🛡️ Brute-Force Indicators

| Field | Details |
|--------|---------|
| **Author** | Prasiddha Pal |
| **Role** | SOC Analyst Trainee |
| **Case ID** | SOC-DAY03-001 |
| **Platform** | Kali Linux |
| **Status** | ✅ Completed |

---

## 🎯 Objective

Identify the indicators of an SSH brute-force attack and understand how SOC analysts differentiate malicious authentication attempts from normal user behavior.

---

## 📖 Concept

A brute-force attack is a technique where a threat actor repeatedly attempts to gain unauthorized access by trying multiple usernames, passwords, or both. SOC analysts detect these attacks by analyzing authentication logs and correlating multiple failed login attempts over a specific period.

---

## 🧪 Indicators of Brute-Force Activity

A potential SSH brute-force attack may include:

- Multiple failed authentication attempts.
- Repeated attempts from the same source IP address.
- Authentication attempts targeting multiple user accounts.
- High login frequency within a short time period.
- Authentication failures followed by a successful login.

---

## 📸 Evidence

### Screenshot – Failed Authentication Events

![Brute Force Indicators](../screenshots/03-bruteforce-indicators.png)

---

## 🔍 Observation

During this investigation:

- Failed SSH authentication events were generated.
- The username **wronguser** did not exist.
- The source IP address was **127.0.0.1**.
- Only a limited number of authentication attempts were observed.
- No successful authentication followed the failed attempts.

---

## 🛡️ SOC Analysis

The observed activity **does not meet the criteria for a brute-force attack**. Although failed authentication events were recorded, they originated from the local system (`127.0.0.1`) during controlled lab testing. There was no evidence of high-frequency authentication attempts, multiple external source IPs, or repeated attacks against numerous user accounts.

A SOC analyst should classify this activity as **expected lab-generated authentication failures**, not a security incident.

---

## 💡 Key Takeaways

- A single failed login is **not** a brute-force attack.
- Correlation is essential before classifying malicious activity.
- Source IP address, event frequency, and timestamps are critical investigation factors.
- Evidence should always support the final conclusion.

---

**Document Version:** 1.0

**Maintained By:** Prasiddha Pal

---
⭐ Part of the **SOC Journey** by **Prasiddha Pal**
