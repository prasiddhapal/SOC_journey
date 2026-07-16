# Practical Notes

## Authentication Logs

Authentication logs record:

- Successful logins
- Failed logins
- SSH authentication
- sudo activity
- PAM events

---

## journalctl

Provides centralized access to logs managed by systemd-journald.

Useful for:

- Authentication
- Services
- Boot events
- System troubleshooting

---

## grep

grep filters large log files to quickly locate relevant security events.

Common options:

- -i → Ignore case
- -n → Show line numbers
- -v → Exclude matching lines
- -c → Count matches
- -E → Extended regular expressions

---

## IOC Correlation

Never rely on a single IOC.

Correlate:

- Authentication
- Process
- Network
- File
- Privileges

before reaching a conclusion.

---

## SOC Workflow

Alert

↓

Verify

↓

Collect Evidence

↓

Correlate IOCs

↓

Analyze

↓

Document

↓

Escalate
