# Day 18 - Notes

## Process Investigation

A process is a running instance of a program.

Every process has:

- PID (Process ID)
- PPID (Parent Process ID)
- User
- CPU Usage
- Memory Usage
- Command

Use `ps` for a snapshot and `top` for real-time monitoring.

---

## ps vs top

| ps | top |
|----|-----|
| Snapshot | Real-time |
| Static output | Dynamic output |
| Good for scripting | Good for monitoring |

---

## CPU & Memory Analysis

High CPU does **not** always mean malware.

Possible causes:

- Backup jobs
- Database queries
- Software updates
- Cryptominers
- Infinite loops

Always investigate before taking action.

---

## Process Hierarchy

Every process has a parent process.

Example:

```text
systemd
 └── sshd
      └── bash
           └── python3
```

Checking the PPID helps identify how a suspicious process started.

---

## Socket Investigation

A socket is an endpoint for network communication.

Use:

```bash
ss
```

to inspect:

- Active connections
- Listening ports
- Established sessions

---

## lsof

Linux treats almost everything as a file.

`lsof` can display:

- Open files
- Open directories
- Network sockets
- Devices

Useful for identifying what resources a process is using.

---

## Linux Signals

| Signal | Description |
|---------|-------------|
| SIGTERM (15) | Graceful termination |
| SIGKILL (9) | Force termination |
| SIGSTOP | Pause process |
| SIGCONT | Resume process |
| SIGHUP | Reload configuration |

Use **SIGTERM** before **SIGKILL** whenever possible.

---

## pgrep vs pkill

| Command | Purpose |
|----------|---------|
| `pgrep` | Find processes |
| `pkill` | Terminate processes |

Example:

```bash
pgrep -a python
```

Finds Python processes without affecting them.

---

## SOC Investigation Workflow

```text
Alert
   ↓
Verify
   ↓
Identify Process
   ↓
Analyze CPU & Memory
   ↓
Inspect Network Activity
   ↓
Collect Evidence
   ↓
Contain
```

---

## Evidence to Collect

Before terminating a process, collect:

- PID
- PPID
- User
- Process path
- CPU usage
- Memory usage
- Open files
- Network connections

---

## Indicators of Suspicious Activity

- High CPU usage
- Running as `root`
- Executing from `/tmp`
- Unknown parent process
- Unexpected outbound connections
- Multiple suspicious child processes

---

## Best Practices

- Verify alerts before responding.
- Avoid killing processes without evidence.
- Correlate process, file, and network activity.
- Preserve evidence during investigations.
- Document every action taken.

---

## Commands Learned

```bash
ps
top
ss
lsof
kill
pgrep
pkill
```

---

## Day 18 Summary

Today's focus was learning how to investigate Linux processes from a SOC analyst's perspective. Instead of memorizing commands, the emphasis was on collecting evidence, validating alerts, and making informed containment decisions.
