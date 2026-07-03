# 🛡️ Failed SSH Authentication

## 🎯 Objective

Generate a failed SSH authentication event and understand how Linux records unsuccessful authentication attempts in the authentication logs.

---

## 📖 Concept

A failed SSH authentication occurs when a user provides invalid credentials or attempts to authenticate using a non-existent account. The SSH daemon (`sshd`) records these events in the authentication logs, providing valuable evidence for SOC analysts to identify unauthorized access attempts and investigate suspicious login activity.

---

## 🧪 Lab Activity

An SSH connection was initiated to the local system using an invalid username.

```bash
ssh wronguser@127.0.0.1
```

An incorrect password was entered multiple times to intentionally generate failed authentication events.

---

## 📸 Evidence

### Screenshot – Failed SSH Authentication

![Failed SSH Authentication](../screenshots/01-failed-ssh-authentication.png)

---

## 🔍 Observation

- An SSH connection was initiated from the local host.
- The username **wronguser** does not exist on the system.
- Multiple failed authentication attempts were recorded.
- The SSH daemon terminated the connection after repeated authentication failures.

---

## 🛡️ SOC Analysis

The investigation confirmed that the authentication attempt targeted a **non-existent user account**. The SSH daemon recorded the event as an **Invalid user** followed by multiple **Failed password** entries before terminating the session. Since the activity originated from the local system (`127.0.0.1`) within a controlled lab environment, it was classified as **expected testing activity** rather than malicious behavior.

---

## 💡 Key Takeaways

- Failed SSH authentication events are recorded in `auth.log`.
- `Invalid user` indicates that the supplied username does not exist.
- `Failed password` confirms unsuccessful authentication.
- Multiple failed attempts should always be investigated to determine whether they indicate user error or potential malicious activity.
