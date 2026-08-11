# Day 21 - Network Investigation

## Objective

Correlate process, DNS, IP, proxy, and file activity to understand suspicious network behavior.

## Investigation Chain

```text
Process
  ↓
DNS Query
  ↓
Resolved IP
  ↓
Network Connection
  ↓
Proxy / Firewall
  ↓
Downloaded File
```

## Example

```text
powershell.exe PID 4820
        ↓
cdn-update.example
        ↓
185.203.44.71
        ↓
TCP/443
        ↓
GET /update.ps1
        ↓
update.ps1
```

## What to Check

- Source host and user
- Process and PID
- Destination IP
- Domain
- Destination port
- DNS activity
- Proxy / firewall logs
- File download
- Connection timing
- Other affected endpoints

## Important Distinction

HTTPS traffic does **not** automatically mean malicious activity.

A downloaded file does **not** automatically prove execution.

An external connection does **not** automatically prove C2.

Each conclusion requires supporting telemetry.

## C2 Investigation

Look for:

- Repeated connections
- Periodic beaconing
- Bidirectional communication
- Command traffic
- Known malicious infrastructure
- Persistence or post-compromise activity

## Key Lesson

> **Correlate process → DNS → IP → network → proxy → file activity before making a conclusion.**

## Status

**Completed ✅**
