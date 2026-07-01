# Day 01 - Linux Authentication Log Analysis

## Document Information

| Field | Details |
|--------|---------|
| **Author** | PRASIDDHA PAL |
| **Role** | SOC Analyst Learner |
| **Challenge** | 100 Days of SOC Analyst |
| **Day** | 01 |
| **Topic** | Understanding `wtmp` & `btmp` |
| **Platform** | Kali Linux |
| **Date** | 01 July 2026 |

---

## 🎯 Objective
Learn how Linux records **successful** and **failed** login attempts.

---

## 📂 Log Files

| File | Purpose |
|------|---------|
| `/var/log/wtmp` | Stores successful logins and logouts |
| `/var/log/btmp` | Stores failed login attempts |

> **Note:** These are **binary files**, so don't use `cat` to read them.

---

## 📌 Useful Commands

View successful logins:

```bash
last
```

View failed login attempts:

```bash
sudo lastb
```

View last login for all users:

```bash
lastlog
```

---

## 🛡️ SOC Scenario

A user reports:

> "I didn't log in at 2:00 AM."

As a SOC Analyst:

1. Check successful logins:

```bash
last
```

2. Check failed login attempts:

```bash
sudo lastb
```

If you see multiple failed logins followed by a successful login from the same IP, it may indicate a **brute-force attack**.

---

## ✅ Key Takeaways

- `wtmp` → Successful logins.
- `btmp` → Failed login attempts.
- Use `last` to read `wtmp`.
- Use `lastb` to read `btmp`.
- These logs help SOC analysts investigate unauthorized access and suspicious login activity.
