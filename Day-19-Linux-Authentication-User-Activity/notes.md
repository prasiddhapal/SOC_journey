# Linux Authentication & User Activity Notes

## Overview

Authentication and user activity analysis are fundamental tasks for SOC analysts. Monitoring user logins, authentication events, processes, and network connections helps identify unauthorized access and potential system compromise.

---

## User Activity Commands

### whoami
Displays the currently logged-in user.

```bash
whoami
```

### who
Shows all active user sessions and login terminals.

```bash
who
```

### id
Displays the user's UID, GID, and group memberships.

```bash
id
```

### groups
Lists all groups assigned to the current user.

```bash
groups
```

### w
Displays active users, uptime, load average, idle time, and currently running commands.

```bash
w
```

---

## Authentication Logs

### last

Displays login history, including login time, logout time, and remote IP address.

```bash
last
```

### journalctl

View authentication logs for SSH.

```bash
sudo journalctl -u ssh
```

Useful searches:

```bash
journalctl | grep Failed
journalctl | grep Accepted
journalctl | grep ssh
```

---

## User Account Investigation

Important files:

- `/etc/passwd`
- `/etc/group`

Useful command:

```bash
getent passwd
```

Check for:

- Unexpected UID 0 accounts
- Unknown users
- Interactive login shells
- Privileged group memberships

---

## SOC Investigation Tips

- Verify login history before investigating processes.
- Correlate failed and successful logins.
- Investigate high CPU or memory usage after suspicious authentication.
- Review active network connections for external communication.
- Preserve evidence before containment whenever possible.

---

## Key Takeaways

- Authentication logs help build an incident timeline.
- User and group auditing detects privilege abuse.
- Process and network analysis reveal attacker activity.
- Multiple indicators together provide stronger evidence than a single event.
