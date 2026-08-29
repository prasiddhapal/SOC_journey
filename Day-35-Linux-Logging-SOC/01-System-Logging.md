# 01 — System Logging

## Objective

Understand how Linux system logs can provide visibility into host activity that is not obvious from authentication events alone.

## Primary log

```text
/var/log/syslog
```

## Investigation examples

The lab used `grep` to search `/var/log/syslog` for time synchronization activity:

```bash
grep -iE 'ntp|timesync|chrony' /var/log/syslog | head -20
```

The logs showed `systemd-timesyncd` contacting the time server:

```text
185.125.190.58:123
```

and performing initial clock synchronization.

## Kernel evidence

Searching for Yama messages showed:

```text
Yama: becoming mindful.
```

## SOC relevance

System logs help analysts understand:

- service starts and stops
- kernel messages
- time synchronization
- system-level errors
- background activity

A single log source rarely explains the complete attack chain.
