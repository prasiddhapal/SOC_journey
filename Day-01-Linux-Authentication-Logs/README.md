# Day 01 - Linux Authentication Log Analysis

## 📌 Objective

The goal of this lab was to understand how Linux records authentication events and how a Security Operations Center (SOC) analyst can investigate login activity using system logs.

During this exercise, I explored Linux authentication logs, identified successful and failed login attempts, analyzed `sudo` activity, and documented my findings as part of a basic incident investigation.

---

## 🎯 Learning Outcomes

By completing this lab, I learned how to:

* Understand the purpose of Linux authentication logs.
* Locate authentication-related log files.
* View and search logs using Linux command-line tools.
* Identify successful and failed login attempts.
* Investigate privilege escalation through `sudo`.
* Create a simple investigation timeline.
* Document findings in a structured format.

---

## 🖥️ Lab Environment

| Component        | Details                                                                 |
| ---------------- | ----------------------------------------------------------------------- |
| Operating System | Kali Linux                                                              |
| Terminal         | Bash                                                                    |
| Log Source       | `/var/log/auth.log` or `journalctl` (depending on system configuration) |
| Tools Used       | grep, tail, less, cat, journalctl                                       |

---

## 📂 Files in this Directory

| File           | Description                                |
| -------------- | ------------------------------------------ |
| `README.md`    | Overview of the lab                        |
| `commands.md`  | Commands executed during the investigation |
| `findings.md`  | Investigation findings                     |
| `timeline.md`  | Chronological timeline of events           |
| `notes.md`     | Personal learning notes                    |
| `screenshots/` | Screenshots of commands and log analysis   |

---

## 🔍 Investigation Process

The investigation followed these steps:

1. Located the Linux authentication logs.
2. Viewed recent authentication events.
3. Searched for SSH login attempts.
4. Identified failed authentication events.
5. Identified successful authentication events.
6. Investigated `sudo` activity.
7. Recorded observations.
8. Created an investigation timeline.
9. Documented all findings.

---

## 🛠️ Commands Practiced

Some of the commands used during this lab included:

* `tail`
* `grep`
* `less`
* `cat`
* `journalctl`

A detailed explanation of each command is available in **commands.md**.

---

## 📊 Key Findings

During this investigation I analyzed:

* Authentication events
* Login attempts
* User activity
* Privilege escalation (`sudo`)
* Session information

Detailed results are available in **findings.md**.

---

## 🧠 Skills Practiced

* Linux Log Analysis
* Authentication Investigation
* SSH Log Analysis
* Privilege Escalation Investigation
* Linux Command Line
* Incident Documentation
* SOC Investigation Fundamentals

---

## 💡 Lessons Learned

This lab demonstrated how authentication logs provide valuable information about user activity and system access. Even a simple review of these logs can reveal failed login attempts, successful authentications, and privileged actions, making them an essential data source for SOC analysts during incident investigations.

---

## 🚀 Next Steps

In Day 02, I will investigate an SSH brute-force scenario by analyzing repeated failed login attempts, identifying the source IP address, reconstructing the attack timeline, and documenting the incident like a SOC Analyst.

---

## 📚 References

* Linux Manual Pages (`man`)
* System Log Documentation
* SSH Documentation

---

**Author:** *PRASIDDHA PAL*

**Challenge:** 100 Days of SOC Analyst
 
**Day:** 01 / 100
