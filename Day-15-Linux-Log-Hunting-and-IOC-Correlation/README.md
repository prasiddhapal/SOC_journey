# Linux Log Hunting & IOC Correlation

## 📖 Introduction

Logs are one of the primary sources of evidence during SOC investigations. This lab focused on Linux authentication logs, log filtering using grep, and IOC (Indicator of Compromise) correlation to investigate suspicious activity before making security decisions.

---

## 🎯 Learning Objectives

- Understand Linux log architecture.
- Investigate authentication events using auth.log and journalctl.
- Filter logs efficiently using grep.
- Learn IOC correlation during SOC investigations.
- Apply an evidence-first investigation methodology.

---

## 📚 Topics Covered

### Linux Logging

- auth.log
- journalctl
- Linux log hierarchy

### Log Hunting

- grep
- grep -i
- grep -n
- grep -v
- grep -c
- grep -E

### IOC Correlation

- Authentication IOC
- Process IOC
- Network IOC
- File IOC
- Privilege IOC

---

## 🛡️ Practical Activities

- Accessed Linux authentication logs.
- Investigated CRON and authentication events.
- Practiced grep-based log filtering.
- Learned IOC correlation using a SOC investigation scenario.
- Followed an evidence-first investigation workflow.

---

## 🎯 Key Takeaways

- Logs provide critical evidence during investigations.
- grep significantly reduces investigation time by filtering relevant events.
- A single IOC is not enough to confirm compromise.
- SOC analysts correlate multiple indicators before escalating an incident.
