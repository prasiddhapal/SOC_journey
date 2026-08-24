# Day 31 - Evidence

## Evidence Source

```text
CyberDefenders Reveal
192-Reveal.dmp
```

## Volatility Evidence

### Memory Profile

```bash
vol -f 192-Reveal.dmp windows.info
```

Purpose: validate the memory image and Windows profile.

### Process Enumeration

```bash
vol -f 192-Reveal.dmp windows.pslist
```

Key finding:

```text
powershell.exe
PID 3692
```

### Process Tree

```bash
vol -f 192-Reveal.dmp windows.pstree
```

Key relationship:

```text
PID 3692
PPID 4120
```

### Command Line

```bash
vol -f 192-Reveal.dmp windows.cmdline --pid 3692
```

Key artifacts:

```text
rundll32.exe
3435.dll
45.9.74.32:8888
davwwwroot
```

### Account Attribution

```bash
vol -f 192-Reveal.dmp windows.getsids --pid 3692
```

Key finding:

```text
Elon
```

## Recommended Screenshots

```text
01-volatility-windows-info.png
02-volatility-pslist.png
03-volatility-pstree.png
04-volatility-cmdline.png
05-volatility-getsids.png
```

## Evidence Standard

Screenshots should contain actual forensic output.

Use the screenshots to support findings rather than using challenge-answer screenshots as the primary evidence.

## Portfolio Value

The evidence demonstrates:

- Memory-image validation
- Process enumeration
- Process-tree analysis
- Command-line analysis
- Account attribution
- IOC extraction
- ATT&CK mapping
- Incident-response reasoning
