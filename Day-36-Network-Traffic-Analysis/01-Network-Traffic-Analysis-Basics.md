# 01 | Network Traffic Analysis Basics

## Objective

Understand why network traffic analysis is an important part of SOC monitoring and incident response.

## What Network Traffic Analysis Provides

Network traffic analysis can help an analyst:

- Detect suspicious or malicious activity
- Reconstruct attacks during incident response
- Validate and investigate alerts
- Identify unusual network behavior
- Investigate potential command-and-control communication
- Detect possible data exfiltration or lateral movement

The training material highlighted DNS tunneling as an example. Multiple DNS queries using different subdomains can look unusual when compared with a normal baseline.

## TCP/IP Visibility

Network communication is encapsulated through several layers:

| Layer | Example Information |
|---|---|
| Application | Protocol headers and application payload |
| Transport | TCP/UDP information, ports, flags, sequence data |
| Internet | Source/destination IP addresses, TTL, fragmentation fields |
| Link | Local addressing such as MAC information |

The critical SOC lesson is that different telemetry sources expose different amounts of information.

## Example: HTTP

An HTTP request can reveal useful metadata such as:

- Requested path
- Host
- User-Agent
- Accepted content
- Connection state

A response can provide additional evidence such as:

- HTTP status
- Content type
- File name
- Content length
- Application data

In the practical scenario, this visibility exposed a PowerShell script download.

## Example: DNS

DNS traffic can reveal:

- Query name
- Record type
- Response data
- Timing
- Source host

TXT records can be particularly interesting during investigations because they can carry application data rather than only traditional address-resolution information.

## Evidence

See:

- `Screenshots/02-traffic-observation.png`
- `Screenshots/04-scenario2-dns-c2-flag.png`

## Analyst Takeaway

Network analysis becomes valuable when the available logs are insufficient to explain what actually happened. The analyst should understand both the protocol and the limitations of the telemetry being reviewed.
