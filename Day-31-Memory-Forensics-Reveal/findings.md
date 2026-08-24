# Day 31 - Findings

## Primary Finding

A malicious `powershell.exe` process was identified in the Windows memory image.

```text
PID: 3692
PPID: 4120
User: Elon
```

## Execution Evidence

The command-line evidence showed suspicious execution involving:

```text
rundll32.exe
```

The second-stage payload was:

```text
3435.dll
```

## Network / Remote Resource Evidence

The activity referenced:

```text
45.9.74.32:8888
```

and:

```text
davwwwroot
```

## ATT&CK

```text
T1218.011 - Rundll32
```

## Malware Family

```text
STRELASTEALER
```

## Assessment

The combined process, account, command-line, payload, and remote-resource evidence supports a compromised-host assessment.

The process should not be considered suspicious from its name alone. The conclusion comes from correlating multiple artifacts.

## Recommended Actions

1. Isolate the affected workstation.
2. Preserve memory and disk evidence.
3. Investigate the `Elon` account.
4. Hunt for `45.9.74.32`.
5. Hunt for `3435.dll`.
6. Review PowerShell telemetry.
7. Investigate PID `4120`.
8. Search other hosts for the same execution pattern.
9. Continue checking for persistence and lateral movement.
