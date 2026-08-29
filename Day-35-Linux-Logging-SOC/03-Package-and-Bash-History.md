# 03 — Package Manager and Bash History

## Objective

Use local host history to identify commands and software installation activity.

## Bash history

The user's Bash history contained:

```bash
sudo apt install zip unzip
```

along with commands used to inspect system logs.

## Package manager evidence

The package logs showed installation of:

```text
unzip:amd64 6.0-28ubuntu4.1
```

The relevant sources were:

```text
/var/log/apt/history.log
/var/log/dpkg.log
```

## Why this matters

Package installation history can support an investigation when an attacker installs tooling or utilities on a compromised host.

Bash history is useful for discovering commands, but it should not be treated as a complete forensic record. Commands may be absent, history can be cleared, and command output is not recorded there.

## SOC correlation

Use:

**Bash history + APT/dpkg logs + authentication logs + audit logs**

to build stronger evidence.
