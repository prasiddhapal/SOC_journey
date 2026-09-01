# 03 - Sudo Investigation

## Search

```spl
index=task5 search sudo
```

## Purpose

The query searches the task index for sudo-related events.

## Why Sudo Matters

Sudo activity can reveal privileged command execution.

Relevant event details can include:

- User
- Target account
- Command
- Session
- Timestamp

## Investigation Example

The practical events showed sudo session creation and closure.

They also showed commands executed as root.

Examples of commands observed in the practical evidence included:

```text
/usr/bin/su
/usr/bin/useradd remote-ssh
/usr/bin/truncate -s 0 /var/log/syslog
```

These commands should be treated as observed evidence.

## Correlation

Privileged commands become more meaningful when correlated with:

- Authentication
- Account creation
- Process execution
- File modification
- Network access

## Analyst Questions

- Who initiated the sudo session?
- Which account became privileged?
- What command was executed?
- When did the session open?
- When did it close?
- Did other suspicious activity occur immediately before or after?

## Documentation Rule

Do not infer intent from a command alone.

Record the command first.

Then correlate surrounding evidence.
