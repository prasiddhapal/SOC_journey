# Day 18 - Interview Questions

## Process Investigation

### Q1. What is the difference between `ps` and `top`?

**Answer**

- `ps` provides a snapshot of running processes.
- `top` provides a real-time view of system activity.

---

### Q2. How do you display detailed information about a process?

```bash
ps -fp <PID>
```

---

### Q3. How do you find the top CPU-consuming processes?

```bash
ps aux --sort=-%cpu | head
```

---

### Q4. How do you find the top memory-consuming processes?

```bash
ps aux --sort=-%mem | head
```

---

## Process Search

### Q5. Difference between:

```bash
pgrep chrome
```

and

```bash
pgrep -a chrome
```

**Answer**

- `pgrep` → Displays PID only.
- `pgrep -a` → Displays PID and full command.

---

### Q6. Why is `pkill python` dangerous?

**Answer**

It may terminate every Python process, including legitimate applications running in production.

---

### Q7. How do you find the newest process?

```bash
pgrep -n <process>
```

---

### Q8. How do you find the oldest process?

```bash
pgrep -o <process>
```

---

## Network Investigation

### Q9. What does `ss` do?

**Answer**

Displays socket and network connection information.

---

### Q10. Which command shows active TCP connections?

```bash
ss -tnp
```

---

### Q11. Which command shows listening ports?

```bash
ss -tulp
```

---

### Q12. What is `lsof` used for?

**Answer**

Lists files and network sockets opened by processes.

---

### Q13. How do you inspect a specific process?

```bash
lsof -p <PID>
```

---

## Process Management

### Q14. Difference between:

```bash
kill
```

and

```bash
kill -9
```

**Answer**

- `kill` sends **SIGTERM** for graceful termination.
- `kill -9` sends **SIGKILL** to force termination.

---

### Q15. Why should `kill -9` be the last option?

**Answer**

It immediately terminates the process without allowing cleanup or graceful shutdown.

---

## SOC Scenario Questions

### Q16. A process is consuming 99% CPU. What is your first step?

**Answer**

Verify the alert using:

```bash
top -p <PID>
```

---

### Q17. You identify:

```text
python3 /tmp/update.py
```

Why is this suspicious?

**Answer**

Because it is executing from `/tmp`, a location commonly abused by attackers for temporary or malicious scripts.

---

### Q18. Which command helps identify active network connections?

```bash
ss -tnp
```

---

### Q19. Which command shows files and sockets opened by a process?

```bash
lsof -p <PID>
```

---

### Q20. A suspicious process has an established outbound connection. What should you do?

**Answer**

1. Collect evidence.
2. Verify the process.
3. Inspect network activity.
4. Contain the process if confirmed malicious.

---

# Quick Revision

| Topic | Command |
|--------|---------|
| Process List | `ps aux` |
| Process Details | `ps -fp <PID>` |
| Live Monitoring | `top` |
| TCP Connections | `ss -tnp` |
| Listening Ports | `ss -tulp` |
| Open Files | `lsof -p <PID>` |
| Find Process | `pgrep -a <name>` |
| Kill Process | `kill <PID>` |

---

# Interview Tips

- Verify before taking action.
- Explain your reasoning, not just the command.
- Correlate process, network, and file evidence.
- Preserve evidence before containment.
- Prefer `SIGTERM` before `SIGKILL`.
