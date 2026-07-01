# Day 01 - Linux Authentication Log Analysis

## Document Information

| Field | Details |
|--------|---------|
| **Author** | PRASIDDHA PAL |
| **Role** | SOC Analyst Learner |
| **Challenge** | 100 Days of SOC Analyst |
| **Day** | 01 |
| **Topic** | Linux Authentication Log Analysis |
| **Platform** | Kali Linux |
| **Date** | 01 July 2026 |
# CASE SCENARIO
#Why SOC Analysts spend most of their day reading logs.
# 🛡️ Why SOC Analysts Spend Most of Their Day Reading Logs

## 🎯 Scenario

Imagine you work as a **SOC (Security Operations Center) Analyst** at **ABC Bank**.

At **2:15 AM**, an employee reports:

> **"I didn't log into the server last night, but someone used my account."**

Your job is to investigate what happened.

You **cannot ask the computer** what happened yesterday.

Instead, you check the **logs**.

Logs are like a **CCTV recording** of the system—they show every important event.

---

## 🔍 Investigation

### Step 1: Check Authentication Logs

```bash
cat /var/log/auth.log
```

You find:

```text
Jul 2 02:11:45 server sshd[1452]: Failed password for alice from 185.45.12.20
Jul 2 02:11:50 server sshd[1454]: Failed password for alice from 185.45.12.20
Jul 2 02:12:10 server sshd[1460]: Accepted password for alice from 185.45.12.20
```

### What does this tell us?

- Two failed login attempts
- Third attempt was successful
- Login came from an unknown IP address

🚩 This could indicate a **brute-force attack** or compromised credentials.

---

### Step 2: Check Sudo Activity

```text
Jul 2 02:13:05 server sudo: alice : COMMAND=/usr/bin/useradd hacker
```

### What does this tell us?

After logging in, the attacker used **sudo** to create a new user.

🚩 Privilege escalation detected.

---

### Step 3: Check System Logs

```text
Jul 2 02:14:18 systemd: Started Apache Web Server.
```

This confirms the system continued running normally after the suspicious activity.

---

## 💡 Why Logs Matter

Without logs:

❌ You wouldn't know:

- Who logged in
- When they logged in
- From where
- What commands they executed
- Whether they gained administrator privileges

With logs:

✅ You can reconstruct the entire attack timeline.

---

## 📊 SOC Analyst Workflow

```text
Alert Received
       │
       ▼
Read Authentication Logs
       │
       ▼
Identify Suspicious Login
       │
       ▼
Check Sudo Activity
       │
       ▼
Review System Logs
       │
       ▼
Confirm Attack Timeline
       │
       ▼
Report & Respond
```

---

## 🎯 Key Takeaway

SOC Analysts spend most of their day reading logs because **logs tell the story of what happened on a system**.

Logs help answer:

- Who logged in?
- When did it happen?
- From which IP address?
- Was the login successful?
- Were administrator privileges used?
- What actions were performed after login?

> **No logs = No evidence.**
>
> **Good logs = Faster detection, investigation, and response to cyber attacks.**

# SCREENSHOT
<img width="627" height="440" alt="image" src="https://github.com/user-attachments/assets/3a018694-c7a8-4921-a4e7-f678a590a82c" />

