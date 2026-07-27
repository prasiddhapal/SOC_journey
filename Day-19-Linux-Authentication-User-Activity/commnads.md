# Linux Authentication & User Activity Commands

This file contains commonly used Linux commands for investigating user activity, authentication events, processes, and network connections during a SOC investigation.

---

# User Information

## Current User

```bash
whoami
```

Displays the current logged-in user.

---

## Active User Sessions

```bash
who
```

Shows logged-in users, login time, and terminal.

---

## User & Group Information

```bash
id
```

Displays:

- UID
- GID
- Group memberships

---

## User Groups

```bash
groups
```

Lists all groups assigned to the current user.

---

## Current User Activity

```bash
w
```

Displays:

- Logged-in users
- Login time
- Idle time
- System uptime
- Load average
- Running commands

---

# Authentication Investigation

## Login History

```bash
last
```

Displays recent login history.

---

## SSH Authentication Logs

```bash
sudo journalctl -u ssh
```

Useful filters:

```bash
journalctl | grep Failed
journalctl | grep Accepted
journalctl | grep ssh
```

---

# User Management

## View User Accounts

```bash
cat /etc/passwd
```

---

## View Groups

```bash
cat /etc/group
```

---

## Query User Information

```bash
getent passwd
```

---

# Process Investigation

## Real-Time Process Monitoring

```bash
top
```

Useful shortcuts:

- `P` → Sort by CPU
- `M` → Sort by Memory

---

## Process Details

```bash
ps -fp <PID>
```

---

## Process Tree

```bash
pstree
```

---

# Network Investigation

## Active Connections

```bash
ss -tunp
```

Shows active TCP/UDP connections and associated processes.

---

## Open Files & Sockets

```bash
lsof -p <PID>
```

Displays files and network sockets opened by a process.

---

# Process Termination

```bash
kill -9 <PID>
```

Terminates a process. Use only after collecting evidence whenever possible.
