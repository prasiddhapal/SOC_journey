# Day 19: Linux Authentication & User Activity Analysis

## 📌 Overview

This lab focuses on investigating Linux authentication events, user activity, running processes, and network connections from a SOC analyst's perspective. The objective is to detect suspicious logins, analyze system activity, and perform a basic incident investigation.

## 🎯 Learning Objectives

- Analyze Linux user activity
- Investigate authentication logs
- Audit user accounts and privileges
- Examine suspicious processes
- Monitor network connections
- Perform a basic SOC investigation

## 🛠️ Commands Covered

```bash
whoami
who
id
groups
w
last
journalctl -u ssh
cat /etc/passwd
cat /etc/group
getent passwd
top
ps -fp <PID>
pstree
ss -tunp
lsof -p <PID>
```

## 🔍 SOC Investigation Workflow

```
Alert
  ↓
last
  ↓
journalctl
  ↓
w
  ↓
top
  ↓
ps
  ↓
ss
  ↓
Containment
```

## 🚨 Indicators of Compromise (IOCs)

- Multiple failed SSH logins
- Successful login from external IP
- Suspicious process (`/tmp/update.py`)
- High CPU usage
- Outbound connection to unknown IP
- Unauthorized user creation

## 📚 Key Takeaways

- Investigate before taking containment actions.
- Correlate logs, processes, and network activity to build a timeline.
- Preserve evidence before terminating suspicious processes.
- Authentication logs are the foundation of Linux incident investigations.

---
**Skills:** Linux Authentication Analysis • User Investigation • Process Analysis • Network Analysis • SOC Investigation • Incident Response
