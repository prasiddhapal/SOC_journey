# 🛡️ Day 02 - Understanding SSH

## 📄 Document Information

| Field | Details |
|--------|---------|
| **Author** | Prasiddha Pal |
| **Role** | SOC Analyst Trainee |
| **Day** | 02 |
| **Topic** | Understanding SSH |
| **Platform** | Kali Linux |
| **Case ID** | SOC-DAY02-001 |
| **Status** | ✅ Completed |

---

# 🎯 Objective

Understand the purpose of SSH, how it works, and why it is important for Linux administration and SOC investigations.

---

# 📖 Background

Modern organizations manage hundreds or even thousands of Linux servers remotely. Physically accessing every server is impractical, so administrators use **Secure Shell (SSH)** to securely connect, execute commands, transfer files, and manage systems over a network.

For SOC analysts, SSH is one of the most monitored services because attackers frequently target it to gain unauthorized access to Linux systems.

---

# 🔍 What is SSH?

**SSH (Secure Shell)** is a secure network protocol used for remote administration of Linux and Unix-based operating systems.

It establishes an encrypted communication channel between a client and a server, ensuring that usernames, passwords, commands, and transferred data remain protected during transmission.

By default, SSH listens on **TCP Port 22**.

---

# ⚙️ How SSH Works

A typical SSH connection follows these steps:

1. The client sends a connection request to the SSH server.
2. The server presents its host key (identity).
3. The client verifies the server's identity.
4. The user authenticates using a password or an SSH key pair.
5. If authentication succeeds, the server creates a secure session.

---

# 🛡️ Why SSH is Important for SOC Analysts

SOC analysts investigate SSH activity to identify:

- Successful remote logins
- Failed authentication attempts
- Brute-force attacks
- Unauthorized remote access
- Privilege escalation after login

SSH logs often provide the first evidence during an incident investigation.

---

# 🧪 Practical Activity

## Command Used

```bash
sudo systemctl status ssh
```

### Purpose

Check whether the SSH service is installed and determine its current operational status.

---

# 📸 Screenshot

**Filename**

`01-ssh-service-status.png`

**Location**

```
Day-02-SSH-Bruteforce-Investigation/
└── screenshots/
    └── 01-ssh-service-status.png
```

Insert the screenshot below.

![SSH Service Status](../screenshots/01-ssh-service-status.png)

---

# 👀 Observation

Initially, the SSH service was inactive. After starting the service, it became available to accept incoming SSH connections.

This confirmed that the system was ready to generate SSH authentication logs for investigation.

---

# 🔎 SOC Analysis

Before investigating authentication events, a SOC analyst should always verify that the service responsible for generating those events is running.

If the SSH service is stopped, no new SSH authentication logs will be produced, making investigation impossible.

Verifying the service status is therefore an essential first step in any SSH-related investigation.

---

# 📚 Key Learning

- SSH provides secure remote administration.
- SSH encrypts communication between client and server.
- SSH listens on TCP Port 22 by default.
- SOC analysts frequently investigate SSH authentication events.
- Service verification should always precede log analysis.

---

# 📌 Revision Box

### Remember

- SSH = Secure Shell
- Default Port = TCP 22
- SSH Server Process = `sshd`
- Used for secure remote administration
- Authentication events are recorded in `auth.log`

---

# 💼 Interview Questions

### Q1. What is SSH?

**Answer:**

SSH (Secure Shell) is a secure network protocol used for remote administration of Linux and Unix systems. It encrypts communication between the client and server and, by default, operates on TCP port 22.

---

### Q2. Why is SSH important for SOC analysts?

**Answer:**

SSH is a common target for attackers attempting unauthorized access. SOC analysts monitor SSH logs to detect successful logins, failed authentication attempts, brute-force attacks, and suspicious remote access.

---

# 🧠 Mentor Notes

### Common Beginner Mistakes

❌ Thinking SSH is only a command.

❌ Confusing the SSH client (`ssh`) with the SSH server (`sshd`).

❌ Starting log analysis without confirming the SSH service is running.

---

# 🎯 Interview Tip

If an interviewer asks:

> "What is SSH?"

Do not answer only:

> "SSH is used for remote login."

Instead, mention:

- Secure protocol
- Remote administration
- Encryption
- TCP Port 22
- Client-server communication

This demonstrates a stronger understanding of the technology.
