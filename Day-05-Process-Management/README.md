# Day 05 – Linux Process Management for SOC Analysts

## 📌 Objective

Learn how Linux manages processes and how SOC analysts investigate suspicious processes during incident response.

---

## 📚 Topics Covered

- Program vs Process
- PID (Process ID)
- PPID (Parent Process ID)
- Process Tree
- ps
- ps -ef
- pstree
- top
- kill
- killall
- Linux Signals
- Background & Foreground Jobs
- SOC Investigation Workflow

---

## 🛠️ Commands Practiced

| Command | Purpose |
|----------|---------|
| ps | Show current terminal processes |
| ps -ef | Show all running processes |
| pstree | Display parent-child process tree |
| top | Monitor processes in real time |
| kill | Gracefully terminate a process |
| kill -9 | Forcefully terminate a process |
| killall | Terminate processes by name |
| jobs | Show background jobs |
| fg | Bring a background job to the foreground |
| bg | Continue a stopped job in the background |
| kill -l | List Linux signals |

---

## 🛡️ SOC Skills Learned

- Investigating high CPU processes
- Identifying parent-child process relationships
- Understanding process ownership
- Using evidence before taking action
- Monitoring processes in real time

---

## 📂 Screenshots

Screenshots are available in the `screenshots/` folder.

---

## 🎯 Key Learning

> Investigate first. Collect evidence. Make a decision. Never assume a process is malicious without evidence.

