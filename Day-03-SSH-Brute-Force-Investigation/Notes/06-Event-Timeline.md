# 🛡️ Event Timeline

| Field | Details |
|--------|---------|
| **Author** | Prasiddha Pal |
| **Role** | SOC Analyst Trainee |
| **Case ID** | SOC-DAY03-001 |
| **Platform** | Kali Linux |
| **Status** | ✅ Completed |

---

## 🎯 Objective

Reconstruct the sequence of authentication events to understand how the SSH authentication attempt progressed from initiation to termination.

---

## 📖 Concept

An event timeline organizes security events in chronological order. SOC analysts use timelines to reconstruct incidents, understand attacker behavior, and correlate authentication events with other security logs.

---

## 📊 Event Timeline

| Step | Security Event | Description |
|------|----------------|-------------|
| 1 | SSH Connection Initiated | Authentication request sent to the SSH server. |
| 2 | Invalid User Identified | SSH daemon detected a non-existent user account (`wronguser`). |
| 3 | Failed Authentication | Authentication failed due to invalid credentials. |
| 4 | Connection Terminated | SSH daemon closed the session after repeated authentication failures. |

---

## 📸 Evidence

### Event Timeline Evidence

![Event Timeline](../screenshots/06-event-timeline.png)

---

## 🔍 Observation

- The authentication attempt originated from **127.0.0.1**.
- The supplied username was invalid.
- Authentication was unsuccessful.
- No SSH session was established.
- The SSH daemon terminated the connection.

---

## 🛡️ SOC Analysis

The reconstructed timeline confirms a complete failed authentication sequence. The events occurred in a logical order without evidence of successful authentication or privilege escalation. Since the activity originated from the local host during controlled testing, it was classified as expected lab activity rather than a security incident.

---

## 💡 Key Takeaways

- Event timelines help reconstruct security incidents.
- Chronological analysis improves investigation accuracy.
- Every authentication event contributes to the overall investigation.
- Timelines support incident reporting and forensic analysis.

---

**Document Version:** 1.0

**Maintained By:** Prasiddha Pal

---
⭐ Part of the **SOC Journey** by **Prasiddha Pal**
