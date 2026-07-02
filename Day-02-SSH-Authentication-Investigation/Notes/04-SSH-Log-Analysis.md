# 🛡️ SSH Log Analysis

## 🎯 Objective

Analyze SSH authentication log entries to identify successful authentication events and extract relevant security information.

---

## 📖 Concept

Linux stores SSH authentication events in `/var/log/auth.log`. These logs contain valuable security information such as the authenticated user, source IP address, authentication method, and session status. SOC analysts review these logs to verify legitimate access and detect suspicious authentication activity.

---

## 🧪 Command

```bash
grep sshd /var/log/auth.log
```

---

## 📸 Evidence

### Screenshot – SSH Authentication Logs

![SSH Authentication Logs](../screenshots/04-ssh-auth-log.png)

---

## 🔍 Observation

- Identified a successful SSH authentication event.
- User **window** was successfully authenticated.
- Authentication method: **Public Key**.
- Source IP Address: **127.0.0.1**.
- SSH session was successfully established.

---

## 🛡️ SOC Analysis

The authentication logs confirmed a successful SSH login originating from the local system (`127.0.0.1`). The user authenticated using the **Public Key** authentication method, and the SSH daemon successfully established a user session. No indicators of unauthorized access or malicious authentication attempts were observed during this investigation.

---

## 💡 Key Takeaways

- `auth.log` records SSH authentication events.
- `Accepted publickey` indicates successful authentication.
- Source IP helps identify where the connection originated.
- Authentication method provides additional investigation context.
- Log analysis is a fundamental SOC investigation skill.
