# 🛡️ SSH Log Analysis

| Field | Details |
|--------|---------|
| **Author** | Prasiddha Pal |
| **Role** | SOC Analyst Trainee |
| **Case ID** | SOC-DAY03-001 |
| **Platform** | Kali Linux |
| **Status** | ✅ Completed |

---

## 🎯 Objective

Analyze SSH authentication logs to identify failed authentication attempts, extract relevant security information, and determine whether the observed activity indicates malicious behavior.

---

## 📖 Concept

Linux records SSH authentication events in `/var/log/auth.log`. These logs contain valuable forensic information such as timestamps, source IP addresses, usernames, authentication status, process IDs (PID), and session details. SOC analysts review these logs to identify suspicious authentication activity and support incident investigations.

---

## 🧪 Lab Activity

Generated failed SSH authentication events using a non-existent user account and analyzed the corresponding log entries.

```bash
ssh wronguser@127.0.0.1
```

Reviewed the authentication logs.

```bash
grep sshd /var/log/auth.log
```

---

## 📸 Evidence

### SSH Authentication Log Entries

![SSH Log Analysis](../screenshots/04-ssh-log-analysis.png)

---

## 🔍 Observation

The authentication logs revealed the following events:

- Source IP Address: **127.0.0.1**
- Username: **wronguser**
- Authentication Status: **Failed**
- Event Type: **Invalid User**
- SSH Daemon terminated the connection after repeated authentication failures.

---

## 🛡️ Evidence Analysis

| Evidence | Analysis |
|----------|----------|
| **Invalid user** | The supplied username does not exist in the local user database. |
| **Failed password** | Authentication using the supplied credentials was unsuccessful. |
| **Connection closed** | The SSH daemon terminated the session after authentication failure. |
| **127.0.0.1** | The authentication attempt originated from the local system (loopback interface). |

---

## 🛡️ SOC Analysis

The investigation confirmed multiple failed authentication attempts targeting a non-existent user account. Although the activity resembled the early stages of a brute-force attack, the evidence indicated that it originated from the local host (`127.0.0.1`) during controlled lab testing. No successful authentication, privilege escalation, or post-authentication activity was observed.

Based on the available evidence, the activity was classified as **expected lab-generated authentication failures** rather than a confirmed security incident.

---

## 💡 Key Takeaways

- Authentication logs provide valuable forensic evidence.
- `Invalid user` and `Failed password` are different authentication events.
- Source IP Address is essential during authentication investigations.
- Evidence correlation is required before declaring malicious activity.

---

**Document Version:** 1.0

**Maintained By:** Prasiddha Pal

---
⭐ Part of the **SOC Journey** by **Prasiddha Pal**
