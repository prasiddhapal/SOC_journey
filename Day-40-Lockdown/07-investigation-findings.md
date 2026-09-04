# Day 40 - Investigation Findings & Analyst Playbook

## Final Case Assessment

The evidence supports a coherent multi-stage compromise of the public-facing IIS server.

### Reconstructed Timeline

```text
11:13+
10.0.2.4 begins reconnaissance against 10.0.2.15
        ↓
Nmap Scripting Engine enumeration
        ↓
SMB share discovery
        ↓
Documents share accessed
        ↓
shell.aspx introduced
        ↓
Reverse shell established toward TCP/4443
        ↓
w3wp.exe provides IIS execution context
        ↓
updatenow.exe executes
        ↓
Startup-folder persistence identified
        ↓
UPX packing confirmed
        ↓
Threat intelligence identifies C2
        ↓
AgentTesla attribution
```

## Investigation Playbook

### 1. Reconnaissance

Check:

- SYN frequency
- Source IP
- Destination IP
- Port diversity
- User-Agent strings
- Scan timing

### 2. SMB Investigation

Check:

- Tree Connect requests
- Share names
- Source/destination
- Authentication context
- File operations

### 3. Web-Shell Investigation

Check:

- HTTP methods
- URI paths
- Uploaded filenames
- Source IP
- Server process
- Timing around exploitation

### 4. Reverse Shell

Check:

- Direction of traffic
- TCP state
- Destination port
- Connection timing
- Parent process
- Child process

### 5. Memory Forensics

Useful Volatility plugins:

```text
windows.info
windows.pstree
windows.cmdline
windows.svcscan
```

### 6. Malware Analysis

Perform:

```text
file
strings
sha256sum
```

Then pivot to threat intelligence.

### 7. C2 Validation

Correlate:

```text
Process
 ↓
DNS
 ↓
Domain
 ↓
IP
 ↓
Port
 ↓
Threat Intelligence
```

## Response Recommendations

In a real enterprise environment, recommended actions would include:

1. Isolate the affected IIS server.
2. Preserve memory, PCAP, malware, and relevant logs.
3. Block confirmed malicious infrastructure where appropriate.
4. Remove the web shell and persistence only after evidence preservation.
5. Hunt for the hash, domain, IP, filename, and related indicators across the environment.
6. Review IIS logs, Windows security logs, process creation telemetry, and authentication activity.
7. Determine whether credentials or additional hosts were compromised.
8. Rebuild the affected server from a trusted image if integrity cannot be established.

## Analyst Lessons

- Start with evidence, not the expected answer.
- Use packet direction and TCP state to reduce noise.
- Process trees provide critical execution context.
- Persistence locations matter.
- Packed malware can defeat simple string searches.
- Hash-based threat intelligence is a powerful pivot.
- Multiple independent indicators produce stronger confidence.
- Document both what the evidence proves and what it does not prove.

## Final Status

**Lockdown Lab: 11/11 Questions Solved**  
**Score: 25/25 Points**  
**Day 40: Completed ✅**
