# SOC Investigation Lab

## Scenario

A SOC analyst receives the following alert:

```
02:12 - Multiple failed SSH login attempts
02:18 - Successful SSH login
02:20 - High CPU usage (98%)
02:21 - Suspicious process: python3 /tmp/update.py
02:22 - Outbound HTTPS connection detected
02:25 - Unauthorized user account created
```

---

# Investigation Steps

## Step 1: Verify Login History

```bash
last
```

Confirm the login time, user, and source IP.

---

## Step 2: Review Authentication Logs

```bash
sudo journalctl -u ssh
```

Look for:

- Failed logins
- Successful logins
- Source IP addresses

---

## Step 3: Check Active Users

```bash
w
```

Identify currently logged-in users and active sessions.

---

## Step 4: Investigate Processes

```bash
top
```

Find processes consuming excessive CPU or memory.

```bash
ps -fp <PID>
```

View detailed information about the suspicious process.

---

## Step 5: Check Network Connections

```bash
ss -tunp
```

Identify active outbound connections and the associated process.

---

## Findings

- Multiple failed SSH login attempts
- Successful login from an external IP
- Suspicious Python script running from `/tmp`
- High CPU utilization
- Outbound connection to an unknown IP
- Unauthorized user account created

---

# Immediate Response

- Isolate the affected host
- Preserve logs and evidence
- Disable compromised accounts
- Remove malicious persistence
- Block malicious IP addresses
- Reset user credentials

---

# Key Takeaways

- Build an incident timeline using multiple data sources.
- Correlate authentication logs with process and network activity.
- Collect evidence before taking containment actions.
- Validate findings before declaring a system compromised.
