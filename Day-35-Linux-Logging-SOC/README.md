# Day 35 — Linux Logging for SOC

## Overview

Day 35 focused on Linux logging and runtime investigation for SOC analysis. The training covered system logs, authentication logs, package-manager history, Bash history, runtime monitoring, system calls, and `auditd`.

The main goal was to move beyond isolated authentication events and reconstruct attacker activity by correlating timestamps, users, processes, commands, files, and network activity.

## Labs / Topics Covered

1. Linux system logging
2. Authentication logs
3. Common Linux logs
4. Runtime monitoring
5. Auditd
6. Bash and package-manager history

## Investigation mindset

A useful investigation flow from this training was:

**Event → timestamp → user → process → command/file/network activity → correlation → attack timeline**

---

## Key Takeaways

- `/var/log/auth.log` is useful for authentication and SSH investigation.
- `/var/log/syslog` provides broader system and service activity.
- Bash history can reveal commands executed by users, but it does not provide complete execution context.
- APT and dpkg logs can reveal package installation activity.
- Runtime monitoring helps answer questions that authentication logs alone cannot.
- `auditd` can provide detailed evidence about process execution, file access, and related system calls.
- Correlation is more valuable than treating a single log entry as the complete story.

## Evidence captured

- SSH authentication activity from suspicious source addresses
- Creation of the `xerxes` user and addition to the `sudo` group
- Installation of `unzip` version `6.0-28ubuntu4.1`
- Bash history containing `sudo apt install zip unzip`
- Access to `/secret.thm`
- Download and execution of `naabu`
- Network scan of `192.168.50.0/24`

## Conclusion

The most important lesson was that Linux SOC investigations require multiple sources. Authentication logs show access, system logs show broader host activity, history files provide command clues, and audit logs can connect processes, users, files, and execution into a timeline.
