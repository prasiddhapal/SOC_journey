# 05 — Auditd Investigation

## Objective

Use `auditd` logs to trace process execution, file access, and related system activity.

## Main tools

The training used:

```bash
ausearch
grep
```

The audit logs can be queried using keys defined in audit rules.

Examples from the training included keys such as:

```text
proc_wget
file_thmsecret
```

## File access evidence

Audit records showed the command:

```bash
cat /secret.thm
```

This demonstrated how a monitored file access can be tied to a process execution event.

## Tool download and execution

Audit evidence showed `wget` downloading:

```text
naabu_2.3.5_linux_amd64.zip
```

The archive was then extracted and the resulting binary was made executable.

The tool was executed with:

```bash
./naabu -host 192.168.50.0/24 -top-ports 4
```

## Network activity

The command indicates a scan against:

```text
192.168.50.0/24
```

using the top four ports.

## Investigation chain

The evidence can be represented as:

```text
wget
  ↓
naabu_2.3.5_linux_amd64.zip
  ↓
unzip
  ↓
chmod +x naabu
  ↓
naabu execution
  ↓
192.168.50.0/24 scan
```

This is a strong example of why process and audit telemetry are useful for reconstructing activity on a Linux host.
