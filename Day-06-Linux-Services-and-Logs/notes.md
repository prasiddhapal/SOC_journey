# Notes

## Linux Service

A Linux service is a background program that provides functionality to the operating system or applications.

Examples:

- ssh
- NetworkManager
- cron
- apache2

---

## systemctl

Used to manage Linux services.

Important difference:

start → Starts immediately.

enable → Starts automatically after boot.

---

## journalctl

Reads logs managed by systemd.

Useful options:

- -n
- -f
- -u

---

## grep

Used to search text.

Useful options:

- -i
- -n
- -c
- -r

---

## Hashing

Hashing verifies file integrity.

Common algorithms:

- MD5
- SHA-256

---

## SOC Investigation Workflow

Alert

↓

Collect Logs

↓

Verify User

↓

Investigate Processes

↓

Correlate Evidence

↓

Escalate

↓

Response
