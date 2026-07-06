# Linux Services & Log Management for SOC Analysts

## Introduction

Linux services and logs play a critical role in system administration and Security Operations Center (SOC) investigations. Services provide essential background functionality, while logs record system events that help analysts investigate incidents, verify activities, and collect forensic evidence.

---

## Learning Objectives

- Understand Linux services and daemons
- Manage services using `systemctl`
- Explore Linux log management
- Investigate logs using `journalctl`
- Monitor log files using `tail`
- Search logs efficiently with `grep`
- Apply Linux commands in SOC investigation scenarios

---

## Topics Covered

### Linux Services
- What is a Service?
- Process vs Service
- Daemon
- systemd
- systemctl

### Service Management
- status
- start
- stop
- restart
- enable
- disable

### Linux Logs
- journalctl
- /var/log
- auth.log
- syslog
- boot.log
- kern.log

### Log Monitoring
- tail
- tail -f

### Log Searching
- grep
- grep -i
- grep -n
- grep -c
- grep -r

### File Integrity
- Hashing
- MD5
- SHA-256

### SOC Investigation
- Authentication Investigation
- Process Investigation
- Log Correlation
- Evidence Collection
- Incident Investigation Workflow

---

## Practical Commands

Refer to `commands.md`

---

## Practical Scenarios

- SSH Authentication Investigation
- Suspicious Service Investigation
- Failed Login Analysis
- Process Investigation
- File Integrity Verification

---

## Interview Preparation

Refer to `interview_questions.md`

---

## Screenshots

All practical demonstrations are available in the `screenshots/` directory.

---

## Key Takeaways

- Services provide continuous background functionality.
- Logs are primary sources of evidence during investigations.
- `systemctl` manages services.
- `journalctl` provides centralized log analysis.
- `grep` enables efficient log searching.
- `tail -f` supports real-time monitoring.
- SOC investigations should always follow an evidence-based approach.
