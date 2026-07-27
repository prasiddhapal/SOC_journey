# Linux Authentication & User Activity Interview Questions

## Technical Interview Questions

### 1. What is the difference between `who` and `w`?

**Answer:**
- `who` displays currently logged-in users and their login terminals.
- `w` provides additional details such as uptime, load average, idle time, CPU usage, and the command each user is running.

---

### 2. What is the purpose of the `id` command?

**Answer:**
The `id` command displays the user's UID, GID, and supplementary group memberships. It helps identify user privileges and access levels.

---

### 3. What information does the `last` command provide?

**Answer:**
It displays user login history, including login time, logout time, session duration, and remote IP addresses.

---

### 4. Why is `journalctl -u ssh` important during an investigation?

**Answer:**
It displays SSH authentication logs, helping analysts identify failed logins, successful logins, brute-force attempts, and unauthorized access.

---

### 5. What is the difference between `/etc/passwd` and `getent passwd`?

**Answer:**
- `/etc/passwd` shows only local user accounts.
- `getent passwd` retrieves user information from both local files and directory services such as LDAP or Active Directory.

---

### 6. Why is a UID of `0` suspicious?

**Answer:**
UID `0` represents the root user. Any unexpected account with UID `0` has full administrative privileges and may indicate privilege escalation or a backdoor account.

---

### 7. Why is `/tmp/update.py` suspicious?

**Answer:**
- Executed from a temporary directory.
- Looks like a fake system update.
- Common attacker location for payloads.
- Often associated with malware execution.
- Correlates with suspicious login activity.

---

### 8. What does `ps -fp <PID>` display?

**Answer:**
It provides detailed process information, including:
- PID
- PPID
- Owner
- Start time
- CPU usage
- Command line

---

### 9. What information does `ss -tunp` provide?

**Answer:**
It displays active TCP/UDP connections, listening ports, remote IP addresses, and the process associated with each connection.

---

### 10. Why shouldn't you immediately kill a suspicious process?

**Answer:**
Because it may destroy valuable forensic evidence. A SOC analyst should collect logs, process details, parent process information, and network connections before containment whenever possible.

---

## HR Interview Questions

### 11. Tell me about yourself.

**Answer:**
"I'm currently building my skills in Linux, SOC operations, and cybersecurity by working on hands-on labs involving authentication analysis, incident response, process investigation, and network analysis. My goal is to become a SOC Analyst where I can apply both technical knowledge and analytical thinking to detect and respond to security incidents."

---

### 12. Why do you want to become a SOC Analyst?

**Answer:**
"I enjoy investigating problems, analyzing logs, and understanding how attacks happen. The SOC role combines technical analysis with continuous learning, which aligns with my career goals in cybersecurity."

---

### 13. How do you handle pressure during an incident?

**Answer:**
"I stay calm, follow the incident response process, prioritize evidence collection, and communicate findings clearly. Following a structured workflow helps avoid mistakes during high-pressure situations."

---

### 14. What are your strengths?

**Answer:**
- Strong analytical thinking
- Quick learner
- Good troubleshooting skills
- Passion for cybersecurity
- Ability to work with Linux and security tools

---

### 15. What is one area you're currently improving?

**Answer:**
"I'm continuously improving my knowledge of incident response, threat hunting, and enterprise SOC tools like Splunk, Microsoft Sentinel, and EDR platforms through hands-on practice."

---

### 16. Why should we hire you?

**Answer:**
"I have a solid foundation in Linux, networking, and SOC fundamentals. I enjoy learning, adapt quickly to new technologies, and focus on solving problems methodically. I'm eager to contribute while continuing to grow as a security professional."

---

### 17. Describe a challenging technical problem you solved.

**Answer:**
"I investigated a simulated Linux compromise by correlating authentication logs, suspicious processes, and network connections. By building an incident timeline, I identified indicators of compromise and recommended appropriate containment actions."

---

### 18. Where do you see yourself in five years?

**Answer:**
"I see myself working as a skilled Security Analyst, handling incident investigations, threat hunting, and eventually progressing into DFIR or Security Engineering while continuing to learn advanced cybersecurity technologies."

---

### 19. How do you keep your cybersecurity knowledge up to date?

**Answer:**
"I regularly practice Linux labs, read security blogs, follow threat reports, complete hands-on projects, and study platforms like TryHackMe, Hack The Box, and MITRE ATT&CK."

---

### 20. Do you have any questions for us?

**Answer:**
Some good questions include:
- What does a typical day look like for a SOC Analyst on your team?
- Which SIEM and EDR tools are used in your SOC?
- How do you support employee learning and certifications?
- What qualities make someone successful in this role?
