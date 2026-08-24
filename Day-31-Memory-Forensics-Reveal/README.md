# Day 31 - Memory Forensics | CyberDefenders Reveal

## Overview
Day 31 moved the SOC journey from SIEM detection into practical memory forensics.

Challenge: CyberDefenders **Reveal**  
Artifact: `192-Reveal.dmp` (~2.1 GB)  
Primary tool: Volatility 3

Objective: identify the malicious process, execution chain, account, payload, remote infrastructure, ATT&CK technique, and malware family.

## Investigation Results

| Question | Finding |
|---|---|
| Q1 | `powershell.exe` |
| Q2 | `4120` |
| Q3 | `3435.dll` |
| Q4 | `davwwwroot` |
| Q5 | `T1218.011` |
| Q6 | `Elon` |
| Q7 | `STRELASTEALER` |

**Result: 7/7 questions completed.**

## Attack Chain

```text
Windows host
  ↓
powershell.exe (PID 3692)
  ↓
Suspicious command
  ↓
45.9.74.32:8888
  ↓
davwwwroot
  ↓
3435.dll
  ↓
rundll32.exe
  ↓
Malicious activity
```

## Key Indicators

```text
Process:        powershell.exe
PID:            3692
PPID:           4120
User:           Elon
Payload:        3435.dll
Remote IP:      45.9.74.32
Remote Port:    8888
Share:          davwwwroot
Utility:        rundll32.exe
ATT&CK:         T1218.011
Malware family: STRELASTEALER
```

## Day Status

```text
Memory analysis: Complete
Attack chain:    Reconstructed
ATT&CK mapping:  Complete
Evidence:        Captured
Questions:       7/7
```
