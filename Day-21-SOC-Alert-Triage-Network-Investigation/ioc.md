# Day 21 - Indicators of Compromise (IOCs)

## IOC Types

- IP Address
- Domain
- URL
- File Hash
- Filename
- File Path
- Process

## Investigation Example

```text
Process:
powershell.exe

File:
update.ps1

Path:
C:\Users\j.smith\AppData\Local\Temp\update.ps1

Domain:
cdn-update.example

IP:
185.203.44.71

URL:
/update.ps1
```

## IOC Correlation

```text
Process
  ↓
File
  ↓
Domain
  ↓
IP
  ↓
Network Activity
```

Correlate IOCs with endpoint, DNS, proxy, firewall, and SIEM telemetry.

## Important

An IOC should be validated before being treated as malicious.

Check:

- Reputation
- Context
- First/last seen
- Related hosts
- Related users
- Historical activity

## Key Lesson

> **An IOC is an investigation lead. Context and correlated evidence determine its significance.**

## Status

**Completed ✅**
