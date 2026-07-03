# 🛡️ Invalid User Attempts

| Field | Details |
|--------|---------|
| **Author** | Prasiddha Pal |
| **Role** | SOC Analyst Trainee |
| **Case ID** | SOC-DAY03-001 |
| **Platform** | Kali Linux |
| **Status** | ✅ Completed |

---

## 🎯 Objective

Understand how Linux records authentication attempts made using non-existent user accounts and why these events are important during security investigations.

---

## 📖 Concept

When an SSH authentication request is received for a username that does not exist in the local user database, the SSH daemon (`sshd`) records an **Invalid user** event. These logs help SOC analysts identify unauthorized access attempts, account enumeration, and potential brute-force activity.

---

## 🧪 Lab Activity

Initiated an SSH connection using a non-existent user account.

```bash
ssh wronguser@127.0.0.1
```

Reviewed the authentication logs to identify the generated event.

```bash
grep "Invalid user" /var/log/auth.log
```

---

## 📸 Evidence

### Invalid User Event

![Invalid User](../screenshots/02-invalid-user.png)

---

## 🔍 Observation

- Authentication attempt targeted the user account **wronguser**.
- The account was not present in the local user database.
- The SSH daemon recorded an **Invalid user** event.
- Authentication was rejected before a session could be established.

---

## 🛡️ SOC Analysis

An **Invalid user** event does **not automatically indicate an attack**. It may result from a typing mistake, an outdated username, or a legitimate configuration issue. However, repeated invalid user attempts targeting multiple account names from the same external IP address may indicate **account enumeration** or the early stages of a brute-force attack. Additional evidence and context are required before classifying the activity as malicious.

---

## 💡 Key Takeaways

- `Invalid user` indicates a non-existent account.
- Not every invalid user event is malicious.
- Always correlate with source IP, timestamps, and event frequency.
- Context is essential before declaring an incident.

---

**Document Version:** 1.0

**Maintained By:** Prasiddha Pal

---
⭐ Part of the **SOC Journey** by **Prasiddha Pal**
