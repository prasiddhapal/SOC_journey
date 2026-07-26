# Process Investigation

## Objective

Learn how to identify, analyze, and investigate running Linux processes from a SOC analyst's perspective.

---

# Process Investigation Workflow

```text
Alert
   ↓
Identify Process
   ↓
Analyze CPU & Memory
   ↓
Check Parent Process
   ↓
Verify Process Path
   ↓
Collect Evidence
   ↓
Contain (If Required)
```

---

# Commands Used

| Command | Purpose |
|---------|---------|
| `ps` | View running processes |
| `ps aux` | Detailed process list |
| `ps -fp <PID>` | Process details |
| `top` | Real-time monitoring |
| `top -p <PID>` | Monitor a specific process |
| `pgrep` | Find process by name |
| `pkill` | Terminate process by name |
| `kill` | Terminate process by PID |

---

# Investigation Checklist

- [ ] Identify the PID
- [ ] Check process owner
- [ ] Review CPU usage
- [ ] Review memory usage
- [ ] Check PPID
- [ ] Verify process path
- [ ] Investigate before killing

---

# Common Investigation Commands

### View All Processes

```bash
ps aux
```

### Top CPU Processes

```bash
ps aux --sort=-%cpu | head
```

### Top Memory Processes

```bash
ps aux --sort=-%mem | head
```

### Inspect a Process

```bash
ps -fp <PID>
```

### Live Monitoring

```bash
top -p <PID>
```

### Find Process

```bash
pgrep -a <process-name>
```

---

# Example Investigation

### Alert

```
High CPU usage detected
```

### Investigation

```bash
top -p 8421
```

↓

```bash
ps -fp 8421
```

Output

```text
python3 /tmp/update.py
```

↓

```bash
pgrep -a python
```

Result

```text
8421 python3 /tmp/update.py
```

---

# Red Flags 🚩

- Running as `root`
- High CPU usage
- Unknown process
- Executing from `/tmp`
- Unexpected parent process
- Multiple instances of same process

---

# Best Practices

- Verify alerts before taking action.
- Preserve evidence whenever possible.
- Prefer `kill` over `kill -9`.
- Understand the process before terminating it.
- Correlate process activity with network connections.

---

# SOC Tips

✅ Check the process owner.

✅ Look for unusual execution paths.

✅ Don't rely only on high CPU usage.

✅ Investigate parent-child relationships.

✅ Collect evidence before containment.
