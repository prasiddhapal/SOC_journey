# Day 40 - PCAP Reconnaissance & Enumeration

## Objective

Identify the source of reconnaissance traffic and determine how the attacker enumerated the IIS host.

## Evidence File

```text
capture.pcapng
```

## Q1 - Reconnaissance Source

Initial packet statistics showed:

- 6,359 packets
- Capture duration: approximately 25 minutes
- IIS host: `10.0.2.15`

The investigation filtered initial TCP SYN packets:

```bash
tshark -r capture.pcapng -Y "tcp.flags.syn==1 && tcp.flags.ack==0" -T fields -e ip.src |
sort | uniq -c | sort -nr
```

The dominant source was:

```text
1075  10.0.2.4
```

The traffic from `10.0.2.4` rapidly probed many destination ports on `10.0.2.15`.

### Q1 Answer

```text
10.0.2.4
```

## Q2 - Enumeration Tool

HTTP request headers were inspected:

```bash
tshark -r capture.pcapng -Y "http.request" -T fields -e frame.time -e ip.src -e ip.dst -e http.request.method -e http.host -e http.user_agent
```

The User-Agent revealed:

```text
Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)
```

### Q2 Answer

```text
Nmap Scripting Engine
```

## Investigation Logic

```text
SYN Flood / Rapid Probing
        ↓
Source IP Frequency
        ↓
10.0.2.4
        ↓
Target IIS Host
        ↓
10.0.2.15
        ↓
HTTP User-Agent
        ↓
Nmap Scripting Engine
```

## Key Lesson

Do not identify reconnaissance from packet volume alone. Correlate source IP, target IP, port diversity, TCP flags, and application-layer metadata.
