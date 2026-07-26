# Network Investigation

## Objective

Learn how to investigate network activity on Linux systems using `ss` and `lsof`.

---

# Investigation Workflow

```text
Suspicious Process
        │
        ▼
Check Active Connections
        │
        ▼
Identify Remote IP
        │
        ▼
Verify Listening Ports
        │
        ▼
Inspect Open Files
        │
        ▼
Collect Evidence
```

---

# Commands Used

| Command | Purpose |
|---------|---------|
| `ss` | Display socket information |
| `ss -t` | Show TCP connections |
| `ss -u` | Show UDP connections |
| `ss -l` | Show listening ports |
| `ss -tulp` | Show listening ports with processes |
| `ss -tnp` | Show active TCP connections with PID |
| `lsof -i` | Display network connections |
| `lsof -iTCP` | Show TCP connections |
| `lsof -iUDP` | Show UDP connections |
| `lsof -p <PID>` | Show files and sockets used by a process |

---

# Common Investigation Commands

### View Active Connections

```bash
ss -tnp
```

### View Listening Ports

```bash
ss -tulp
```

### Find Process Using a Port

```bash
sudo lsof -i :22
```

### Inspect Process Connections

```bash
lsof -p <PID>
```

---

# Example Investigation

### Alert

```
Suspicious python3 process detected
```

### Step 1

```bash
ss -tnp
```

Output

```text
ESTAB 192.168.1.20:45231 → 185.199.111.153:443
```

---

### Step 2

```bash
lsof -p 8421
```

Output

```text
python3
TCP 192.168.1.20:45231 -> 185.199.111.153:443
```

---

# Red Flags 🚩

- Unknown external IP
- Unexpected listening port
- Reverse shell connection
- Multiple outbound connections
- High network activity
- Root-owned process with network access

---

# SOC Investigation Checklist

- [ ] Check active connections
- [ ] Identify remote IP
- [ ] Verify process ownership
- [ ] Inspect open sockets
- [ ] Look for unusual ports
- [ ] Preserve evidence
- [ ] Contain if malicious

---

# Best Practices

- Investigate before terminating a process.
- Correlate network activity with process information.
- Verify whether the connection is expected.
- Document suspicious IP addresses.
- Collect evidence before containment.

---

# SOC Tips

✅ Use `ss` for live network analysis.

✅ Use `lsof` to identify which process owns a connection.

✅ Verify external connections before taking action.

✅ Investigate unusual listening ports.

✅ Always correlate process and network evidence.
