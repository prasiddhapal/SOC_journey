# 📝 Learning Notes

| Field | Details |
|--------|---------|
| **Author** | Prasiddha Pal |
| **Role** | SOC Analyst Trainee |
| **Case ID** | SOC-DAY03-001 |
| **Platform** | Kali Linux |
| **Status** | ✅ Completed |

---

# 🎯 Objective

Summarize the key concepts, commands, and technical terms learned during the SSH Brute Force Investigation for quick revision.

---

## 📚 Key Concepts

- Failed SSH Authentication
- Invalid User
- Failed Password
- SSH Authentication Logs
- Brute Force Indicators
- Event Timeline
- Evidence Correlation
- False Positive

---

## 🛠 Commands Practiced

```bash
sudo systemctl status ssh
ssh wronguser@127.0.0.1
grep sshd /var/log/auth.log
grep "Invalid user" /var/log/auth.log
grep "Failed password" /var/log/auth.log
```

---

## 🔍 Important Log Entries

```text
Invalid user
Failed password
Connection closed
PAM authentication failure
```

---

## 💡 Technical Terms Learned

- SSH Daemon (`sshd`)
- Authentication Failure
- Invalid User
- Loopback Address
- Ephemeral Source Port
- Event Correlation
- Risk Assessment
- False Positive

---

## 🧠 Key Learnings

- Authentication logs provide valuable forensic evidence.
- Every failed login is not a brute-force attack.
- Evidence correlation is essential before confirming an incident.
- Source IP, timestamps, and authentication patterns should always be analyzed together.
- SOC analysts make evidence-based decisions instead of assumptions.

---

## 📌 Daily Summary

Today, I generated failed SSH authentication events in a controlled Kali Linux lab and analyzed the resulting authentication logs. I learned how to identify invalid user attempts, distinguish normal authentication failures from brute-force indicators, reconstruct an event timeline, and document the investigation using evidence-based analysis.

---

**Document Version:** 1.0

**Maintained By:** Prasiddha Pal

---
⭐ Part of the **SOC Journey** by **Prasiddha Pal**
