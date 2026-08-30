# 05 | Key Findings and SOC Notes

## Executive Summary

The Day 36 exercises demonstrated how network traffic analysis can move an investigation beyond basic connection logs and into protocol-level evidence.

Two practical findings were identified:

1. A malicious PowerShell download was visible through HTTP packet inspection.
2. A DNS response exposed command-and-control information.

## Finding 01 | Malicious PowerShell Download

**Evidence:** `Screenshots/03-scenario1-malicious-ps-download.png`

The packet capture showed an HTTP response with a successful `200 OK` status and a downloaded `install.ps1` file.

**Flag:** `THM{FoundTheMalware}`

### Security Significance

A PowerShell script delivered through an HTTP download can represent an important execution or initial-access indicator. In a real investigation, the analyst would correlate:

- Source and destination IPs
- Timestamp
- URL/request path
- User-Agent
- Downloaded filename
- Endpoint process activity
- PowerShell logging
- File hashes, where available

## Finding 02 | DNS C2 Information

**Evidence:** `Screenshots/04-scenario2-dns-c2-flag.png`

A DNS response contained a TXT record with:

**Flag:** `THM{C2CommandFound}`

### Security Significance

DNS can be abused as a communication mechanism. Suspicious DNS activity should be assessed using volume, frequency, domain characteristics, record type, response contents, and host context.

## Evidence Quality Standard

A professional SOC record should avoid collecting screenshots without context.

Each evidence item should answer:

- What happened?
- Where did it happen?
- Which telemetry proves it?
- Why is it suspicious?
- What should be investigated next?

## Recommended Correlation

For a real incident, the network evidence should be correlated with:

- Firewall logs
- DNS logs
- Proxy logs
- Endpoint telemetry
- Process creation events
- PowerShell logs
- Authentication events
- File creation events

## Key Lessons

### 1. Visibility is a design decision

The monitoring point determines what can be observed.

### 2. Packet data can expose application context

HTTP and DNS inspection can reveal information that connection metadata alone cannot provide.

### 3. East-West traffic matters

After compromise, attackers may move internally rather than communicating only with external infrastructure.

### 4. Flow data and packet capture complement each other

NetFlow/IPFIX can identify communication patterns, while packet capture can provide deeper protocol-level context.

### 5. Evidence must be interpretable

The best evidence is not necessarily the largest screenshot. It is the smallest set of screenshots that clearly demonstrates the finding.

## Final Assessment

Day 36 provided practical exposure to network visibility and packet analysis. The exercises reinforced the SOC workflow of **collecting appropriate telemetry, inspecting protocol-specific evidence, identifying suspicious behavior, and correlating findings with additional sources**.
