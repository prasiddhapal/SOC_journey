# Linux Authentication Logs

Authentication logs help SOC analysts detect unauthorized access, failed login attempts, and suspicious authentication activity.

---

# Login History

## last

```bash
last
```

Displays:

- Username
- Login time
- Logout time
- Session duration
- Remote IP address

Useful for verifying user login history during an investigation.

---

# SSH Authentication Logs

```bash
sudo journalctl -u ssh
```

Displays SSH service logs, including successful and failed login attempts.

Useful filters:

```bash
journalctl | grep Failed
```

Shows failed authentication attempts.

```bash
journalctl | grep Accepted
```

Shows successful logins.

```bash
journalctl | grep ssh
```

Displays all SSH-related events.

---

# What to Look For

During an investigation, review:

- Multiple failed login attempts
- Successful login after repeated failures
- Logins from unknown IP addresses
- Logins outside normal working hours
- Unexpected root or privileged user logins

---

# SOC Investigation Workflow

```text
Authentication Alert
        │
        ▼
Check Login History
(last)
        │
        ▼
Review SSH Logs
(journalctl)
        │
        ▼
Identify Suspicious User
        │
        ▼
Investigate Running Processes
        │
        ▼
Review Network Connections
```

---

# Common Indicators of Compromise (IOCs)

- Brute-force login attempts
- Successful login from an unfamiliar IP
- Multiple authentication failures
- New privileged user login
- Authentication followed by suspicious process execution

---

# Best Practices

- Correlate authentication logs with process and network activity.
- Investigate successful logins after multiple failures.
- Verify the legitimacy of external login sources.
- Preserve logs before performing containment actions.
