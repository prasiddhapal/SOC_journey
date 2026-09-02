# WTMP Session Correlation

## Why WTMP Matters
`auth.log` records authentication and PAM events. The investigation required the timestamp of the attacker's interactive terminal session, which is available in `wtmp`.

## Command
```bash
TZ=UTC python3 utmp.py wtmp | grep "65.2.161.68"
```

The `TZ=UTC` setting prevents the parser's local-time conversion from producing a misleading timestamp.

## Finding
Interactive root session:

`2024-03-06 06:32:45 UTC`

Authentication occurred at `06:32:44`, one second earlier. These are different events.

Corresponding SSH session number:

`37`

## SOC Lesson
Authentication time and terminal-session start time should not automatically be treated as identical during incident reconstruction.

## Evidence Screenshot
**Evidence 02 - WTMP Interactive Root Session in UTC**
