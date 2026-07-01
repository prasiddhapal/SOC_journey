# Day 01 - Linux Authentication Log Analysis

## Document Information

| Field | Details |
|--------|---------|
| **Author** | Your Name |
| **Role** | SOC Analyst Learner |
| **Challenge** | 100 Days of SOC Analyst |
| **Day** | 01 |
| **Topic** | Linux Authentication Log Analysis |
| **Platform** | Kali Linux |
| **Date** | 01 July 2026 |

---
## 🎯 Objective
Learn where Linux stores log files and why they are important in cybersecurity.

## 📖 What are Linux Logs?
Linux logs are files that record system activities such as:
- User logins
- System events
- Errors
- Service activity
- Security events

Think of logs as the **diary of a Linux system**.

## 📂 Where are Logs Stored?
Most Linux logs are stored in:

```bash
/var/log/
```

## 📄 Common Log Files

| Log File | Purpose |
|----------|---------|
| `/var/log/auth.log` | Authentication logs (Ubuntu/Debian) |
| `/var/log/secure` | Authentication logs (RHEL/CentOS) |
| `/var/log/syslog` | General system logs |
| `/var/log/kern.log` | Kernel logs |
| `/var/log/boot.log` | Boot logs |

## 🔍 Useful Commands

List log files:

```bash
ls /var/log
```

View a log:

```bash
cat /var/log/syslog
```

View recent entries:

```bash
tail /var/log/syslog
```

Search inside logs:

```bash
grep ssh /var/log/auth.log
```

## 💡 Why are Logs Important?

Logs help SOC analysts answer:
- Who logged in?
- When did it happen?
- Was it successful?
- What errors occurred?
- Was there any suspicious activity?

## ✅ Key Takeaway

- Linux stores most logs in **`/var/log/`**.
- Logs record system and security events.
- They are essential for troubleshooting and incident investigations.
