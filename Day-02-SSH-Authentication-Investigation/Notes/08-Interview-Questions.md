# 🛡️ Day 02 - Interview Questions & Answers

## 🎯 Objective

Revise the key concepts covered in the SSH authentication investigation and prepare for SOC Analyst interviews.

---

## Q1. What is SSH?

**Answer:**

SSH (Secure Shell) is a secure network protocol used for remote administration of Linux and Unix systems. It encrypts communication between the client and server, ensuring confidentiality and integrity. By default, SSH uses **TCP Port 22**.

---

## Q2. What is SSHD?

**Answer:**

SSHD (Secure Shell Daemon) is the server-side process responsible for accepting incoming SSH connections, authenticating users, and establishing secure remote sessions.

---

## Q3. Why is SSH important for SOC Analysts?

**Answer:**

SOC analysts investigate SSH because it is commonly targeted by attackers for unauthorized remote access. SSH logs help identify successful logins, failed authentication attempts, brute-force attacks, and suspicious remote access activity.

---

## Q4. Which command is used to verify the SSH service?

```bash
sudo systemctl status ssh
```

**Answer:**

This command verifies whether the SSH service is operational before analyzing authentication logs.

---

## Q5. Which command verifies that SSH is listening on Port 22?

```bash
ss -tlnp | grep :22
```

**Answer:**

This command confirms that the SSH daemon is actively listening for incoming connections on **TCP Port 22**.

---

## Q6. Where are SSH authentication logs stored?

**Answer:**

SSH authentication events are commonly stored in:

```text
/var/log/auth.log
```

(Some Linux distributions may use the systemd journal instead.)

---

## Q7. Which command displays SSH authentication logs?

```bash
grep sshd /var/log/auth.log
```

**Answer:**

This command filters SSH-related authentication events from the authentication log.

---

## Q8. What does the following log indicate?

```text
Accepted publickey for window from 127.0.0.1 port 36698 ssh2
```

**Answer:**

This log confirms a successful SSH authentication.

- Authenticated Account: **window**
- Authentication Mechanism: **Public Key**
- Source IP Address: **127.0.0.1**
- SSH Protocol Version: **SSHv2**

---

## Q9. What does `127.0.0.1` represent?

**Answer:**

`127.0.0.1` is the **loopback (localhost) IP address**, indicating that the SSH connection originated from the same system.

---

## Q10. What is the difference between Port 22 and Port 36698?

**Answer:**

- **Port 22** is the destination port where the SSH server listens.
- **Port 36698** is the client's temporary (ephemeral) source port, automatically assigned for that session.

---

## Q11. What does `Accepted publickey` mean?

**Answer:**

It indicates that the user was successfully authenticated using the **Public Key Authentication** mechanism.

---

## Q12. What information can a SOC analyst extract from an SSH authentication log?

**Answer:**

A SOC analyst can identify:

- Authenticated Account
- Source IP Address
- Authentication Mechanism
- Authentication Status
- Session Information
- Timestamp
- Process ID (PID)

---

## Q13. What should a SOC analyst verify before analyzing SSH logs?

**Answer:**

Before log analysis, the analyst should verify that:

- The SSH service is operational.
- The service is listening on TCP Port 22.
- Authentication events are being generated.

---

## 📌 Quick Revision

| Topic | Remember |
|--------|----------|
| SSH | Secure Shell |
| SSHD | SSH Daemon |
| Default Port | TCP 22 |
| Log File | `/var/log/auth.log` |
| Success | `Accepted publickey` |
| Localhost | `127.0.0.1` |
| Service Check | `systemctl status ssh` |
| Log Analysis | `grep sshd /var/log/auth.log` |
