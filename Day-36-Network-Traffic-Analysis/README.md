# Day 36 | Network Traffic Analysis

## Overview

Day 36 focused on the fundamentals of **network traffic analysis** from a SOC analyst perspective. The work moved from understanding what network traffic contains to identifying useful traffic sources, selecting appropriate collection points, and interpreting packet-level evidence.

The practical portion focused on **full packet capture, network TAP placement, HTTP traffic inspection, DNS traffic analysis, and network-flow visibility**.

The objective was not simply to obtain flags. The more important outcome was learning how a SOC analyst decides **where visibility is needed, what telemetry is available, and what evidence can support an investigation**.

---

## Learning Objectives

- Understand the role of network traffic analysis in security monitoring.
- Identify information available at the application, transport, internet, and link layers.
- Distinguish endpoint and intermediary traffic sources.
- Understand North-South and East-West network flows.
- Compare logs, full packet capture, and network statistics.
- Understand network TAPs and port mirroring as traffic-collection methods.
- Recognize the investigative value of HTTP and DNS traffic.
- Understand how NetFlow/IPFIX provide flow metadata rather than complete packet contents.

---

## Core Concepts

### 1. Network Traffic Analysis

Network traffic analysis combines available network telemetry to identify abnormal communication, reconstruct activity, validate alerts, and investigate suspicious behavior.

Examples from the lab material include:

- DNS tunneling and beaconing
- Suspicious HTTP downloads
- Command-and-control communication
- Data exfiltration
- Lateral movement
- Session hijacking indicators
- Fragmentation-based IDS evasion

### 2. TCP/IP Visibility

Traffic is encapsulated across multiple layers:

- **Application:** application headers and payload
- **Transport:** TCP/UDP headers and ports
- **Internet:** IP addressing and related fields
- **Link:** local network addressing information

The amount of information available depends on the telemetry source. Logs may expose only selected fields, while a full packet capture can provide much deeper context.

### 3. Traffic Sources and Flows

Network sources can be grouped into:

- **Endpoint sources:** hosts, servers, IoT devices, printers, cloud resources, mobile devices, and similar systems.
- **Intermediary sources:** firewalls, switches, routers, proxies, IDS/IPS, access points, and related infrastructure.

Traffic flows can be grouped into:

- **North-South:** traffic entering or leaving the LAN.
- **East-West:** traffic occurring within the LAN, including LAN-to-cloud communication.

### 4. Full Packet Capture

Full packet capture provides detailed visibility into network communication. The lab introduced two ways to obtain it:

- Network TAP
- Port mirroring

A TAP copies traffic without changing the original communication path. Port mirroring duplicates traffic from a switch interface to a monitoring interface.

### 5. Network Statistics

**NetFlow** and **IPFIX** provide flow metadata rather than complete packet contents. This can still be valuable for detecting:

- Command-and-control traffic
- Data exfiltration
- Lateral movement
- Abnormal communication patterns

---

## Practical Investigation

### Scenario 1: Malicious PowerShell Download

The first practical scenario involved a workstation that had initiated an HTTP request after a phishing interaction.

The correct TAP placement was **WP1**. Once the TAP was placed correctly, packet visibility exposed the HTTP response.

The captured response showed:

- Source: `203.0.113.200`
- Destination: `192.168.0.3`
- Protocol: TCP/HTTP
- HTTP status: `200 OK`
- Downloaded file: `install.ps1`
- Flag: `THM{FoundTheMalware}`

This demonstrates why traffic visibility matters. A conventional log might indicate a connection, while packet inspection can expose the actual downloaded object and provide stronger evidence of malicious activity.

### Scenario 2: DNS C2 Traffic

The second scenario demonstrated how DNS can carry command-and-control information.

The DNS response contained a TXT record whose data exposed:

`THM{C2CommandFound}`

This is representative of a broader SOC detection problem: DNS can appear normal at a high level while the content and frequency of queries reveal suspicious behavior.

---

## Evidence Index

| Evidence | Description | Security Value |
|---|---|---|
| 01 | Task 5 network-traffic analysis section | Establishes the investigation context |
| 02 | Network traffic observation concepts | Shows TCP/IP visibility and packet-level analysis |
| 03 | Correct TAP placement and malicious HTTP response | Demonstrates collection-point selection and malware download visibility |
| 04 | DNS response containing C2 flag | Demonstrates DNS-based C2 investigation |
| 05 | Traffic-analysis practical exercise | Documents the hands-on TAP/packet-analysis workflow |

Detailed evidence notes are available in the individual Markdown files.

---

## Tools and Technologies

- Network TAP
- Port Mirroring
- Packet capture / packet inspection
- HTTP
- DNS
- TCP/IP
- NetFlow
- IPFIX
- Wireshark
- TCPDump
- IDS/IPS concepts

---

## SOC Analyst Takeaways

1. **Visibility must be intentional.** The location of a TAP or mirror determines which traffic can be inspected.
2. **Logs are useful but incomplete.** Packet capture can provide application-level context that ordinary logs may omit.
3. **DNS deserves investigation.** Query names, record types, timing, and response contents can expose suspicious communication.
4. **Network evidence should be correlated.** Source/destination IPs, ports, timestamps, protocols, and application data together provide stronger investigative context.
5. **Flow telemetry complements packet capture.** NetFlow/IPFIX can identify communication patterns even when complete packet contents are unavailable.
6. **Evidence should support a conclusion.** A good investigation records what was observed, why it is suspicious, and what additional telemetry should be checked.

---

## Conclusion

Day 36 strengthened the practical side of network investigation. The key lesson was that effective SOC monitoring depends on selecting the right telemetry and understanding what that telemetry can actually prove.

The exercises demonstrated two important investigation paths: inspecting HTTP traffic to identify a malicious PowerShell download, and examining DNS traffic to identify command-and-control information.

The result is a more structured approach to network investigations: **identify the traffic source, understand the flow, collect the right visibility, inspect the relevant protocol fields, and preserve the evidence that supports the finding.**
