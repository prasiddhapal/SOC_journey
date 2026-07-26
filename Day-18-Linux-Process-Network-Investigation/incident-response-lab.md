# Linux SOC Investigation Lab

## Scenario

A SIEM alert reported unusually high CPU usage on a Linux server.

**Alert Details**

| Field | Value |
|-------|-------|
| Severity | High |
| Host | linux-app-01 |
| Process | python3 |
| PID | 8421 |
| CPU Usage | ~99% |

---

# Investigation Workflow

```text
Alert
   │
   ▼
Verify Process
   │
   ▼
Analyze Process
   │
   ▼
Investigate Network
   │
   ▼
Collect Evidence
   │
   ▼
Classify Incident
   │
   ▼
Contain Threat
```

---

# Step 1 - Verify Alert

```bash
top -p 8421
```

### Finding

- CPU usage remained around **99%**
- Alert confirmed

---

# Step 2 - Analyze Process

```bash
ps -fp 8421
```

Output

```text
python3 /tmp/update.py
```

### Findings

- Running as **root**
- Executing from **/tmp**
- Suspicious filename

---

# Step 3 - Investigate Network Activity

```bash
ss -tnp
```

### Finding

```text
ESTABLISHED
192.168.1.20 → 185.199.111.153:443
```

---

# Step 4 - Inspect Open Files

```bash
lsof -p 8421
```

### Findings

- Process working directory: `/tmp`
- Active outbound TCP connection
- Python interpreter in use

---

# Indicators of Compromise (IOCs)

- High CPU usage
- Process running as root
- Script executed from `/tmp`
- Outbound connection to external IP
- Suspicious process name (`update.py`)

---

# Evidence Collected

- Process information
- PID and PPID
- CPU utilization
- Network connection
- Execution path
- User context

---

# Incident Classification

**Result:** ✅ True Positive

### Reason

The process was consuming excessive CPU, running from an unusual location (`/tmp`), executing as `root`, and maintaining an outbound connection to an external IP address.

---

# Containment

Recommended approach:

```bash
kill 8421
```

If the process does not terminate:

```bash
kill -9 8421
```

> Always collect evidence before terminating a suspicious process.

---

# Lessons Learned

- Validate alerts before responding.
- Investigate the process path.
- Correlate process and network activity.
- Preserve evidence before containment.
- Avoid terminating processes without verification.

---

# Skills Practiced

- Process investigation
- Live process monitoring
- Network analysis
- Evidence collection
- Incident classification
- Threat containment
