# 🛡️ Commands Reference

| Field | Details |
|--------|---------|
| **Author** | Prasiddha Pal |
| **Role** | SOC Analyst Trainee |
| **Case ID** | SOC-DAY03-001 |
| **Platform** | Kali Linux |
| **Status** | ✅ Completed |

---

## 🎯 Objective

Maintain a quick reference of the Linux commands used during the SSH authentication investigation.

---

## 🧪 Commands Reference

| Command | Purpose | SOC Use Case |
|---------|---------|--------------|
| `sudo systemctl status ssh` | Verify SSH service status | Confirm the SSH service is operational before investigating logs. |
| `ssh wronguser@127.0.0.1` | Generate a failed SSH authentication event | Simulate failed login attempts for analysis. |
| `grep sshd /var/log/auth.log` | Display SSH-related log entries | Review SSH authentication events. |
| `grep "Invalid user" /var/log/auth.log` | Filter invalid user events | Identify authentication attempts targeting non-existent accounts. |
| `grep "Failed password" /var/log/auth.log` | Display failed authentication attempts | Detect repeated login failures. |

---

## 🛡️ Expected Output

During this investigation, the following log entries were observed:

```text
Invalid user wronguser from 127.0.0.1
Failed password for invalid user wronguser
Connection closed by invalid user wronguser
```

These log entries confirmed that the authentication attempt targeted a non-existent user account.

---

## 💡 Key Takeaways

- `systemctl` verifies the operational status of services.
- `ssh` can be used to generate authentication events in a lab environment.
- `grep` helps filter relevant log entries during investigations.
- Command-line tools enable efficient authentication log analysis.

---

**Document Version:** 1.0

**Maintained By:** Prasiddha Pal

---
⭐ Part of the **SOC Journey** by **Prasiddha Pal**
