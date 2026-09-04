# Day 40 | CyberDefenders Lockdown

> **Case Type:** Network Forensics / DFIR Investigation  
> **Severity:** 🔴 High  
> **Status:** 🟢 Investigation Complete  
> **Platform:** CyberDefenders  
> **Lab:** Lockdown  
> **Environment:** Authorized Security Lab

---

## Executive Summary

Day 40 focused on reconstructing a multi-stage compromise of a public-facing IIS server using three evidence sources:

- PCAP network traffic
- Windows memory image
- Malicious executable sample

The investigation moved from reconnaissance and service enumeration into SMB share discovery, web-shell deployment, reverse-shell activity, memory forensics, persistence analysis, and malware/threat-intelligence attribution.

The investigation was completed with **11/11 questions solved and 25/25 points**.

## Attack Chain

```text
Reconnaissance
    ↓
TCP SYN Port Probing
    ↓
Nmap Scripting Engine Enumeration
    ↓
SMB Share Discovery
    ↓
shell.aspx Web-Shell Upload
    ↓
Reverse Shell on TCP/4443
    ↓
IIS w3wp.exe Context
    ↓
updatenow.exe Persistence
    ↓
Startup Folder Execution
    ↓
UPX-Packed Malware
    ↓
C2: cp8n1.hyperhost.ua
    ↓
AgentTesla Attribution
```

## Key Findings

| Area | Finding |
|---|---|
| Recon source | `10.0.2.4` |
| IIS host | `10.0.2.15` |
| Enumeration tool | Nmap Scripting Engine |
| First SMB shares | `\10.0.2.15\IPC$`, `\10.0.2.15\Documents` |
| Web shell | `shell.aspx` |
| Reverse-shell port | `4443` |
| Kernel base | `0xf80079213000` |
| Persistent executable | `updatenow.exe` |
| Full path | `C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup\updatenow.exe` |
| Parent process | `w3wp.exe` |
| Parent PID | `4332` |
| Packer | UPX |
| SHA-256 | `c25a6673a24d169de1bb399d226c12cdc666e0fa534149fc9fa7896ee61d406f` |
| C2 FQDN | `cp8n1.hyperhost.ua` |
| Malware family | AgentTesla |

## Analyst Principle

> **Correlate network, memory, process, persistence, and threat-intelligence evidence before making an attribution.**

## Evidence

See the `Screenshots/` directory for the strongest evidence captured during the investigation.

## Status

**Day 40 - Completed ✅**
