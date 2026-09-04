# Day 40 - Threat Intelligence, C2 & Malware Attribution

## Objective

Use the sample hash and VirusTotal relationships/behavior to identify the C2 FQDN and malware family.

## Q10 - C2 FQDN

The sample hash was searched in VirusTotal.

VirusTotal Relations showed a suspicious contacted domain:

```text
cp8n1.hyperhost.ua
```

The Behavior section independently showed the same domain under:

- SMTP Communications
- DNS Resolutions
- IP Traffic
- Memory Pattern Domains

The associated IP traffic included:

```text
185.174.175.187:587
```

### Q10 Answer

```text
cp8n1.hyperhost.ua
```

## Q11 - Malware Family

VirusTotal detection results associated the sample with:

```text
Trojan.Win32/AgentTesla...
```

The malware family is:

```text
AgentTesla
```

### Q11 Answer

```text
AgentTesla
```

## Confidence Assessment

The attribution was not based on one antivirus label alone.

Evidence chain:

```text
SHA-256
   ↓
VirusTotal sample
   ↓
Malicious detections
   ↓
Network relationships
   ↓
cp8n1.hyperhost.ua
   ↓
AgentTesla family detection
```

## Key Lesson

Threat intelligence is strongest when used as a correlation source rather than a replacement for local evidence.

A reputation result should be validated against:

- Network telemetry
- DNS activity
- Process context
- File hash
- Persistence
- Memory evidence
- Malware behavior

## IOC Summary

| Type | Indicator |
|---|---|
| Source IP | `10.0.2.4` |
| Compromised IIS | `10.0.2.15` |
| Reverse shell | TCP `4443` |
| File | `shell.aspx` |
| Persistent executable | `updatenow.exe` |
| SHA-256 | `c25a6673a24d169de1bb399d226c12cdc666e0fa534149fc9fa7896ee61d406f` |
| C2 FQDN | `cp8n1.hyperhost.ua` |
| C2 IP | `185.174.175.187` |
| Malware family | AgentTesla |
