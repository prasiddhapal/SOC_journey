# 03 | TAP, Port Mirroring and Full Packet Capture

## Objective

Document how full packet visibility can be obtained and how the correct collection point affects an investigation.

## Full Packet Capture

The training material introduced two primary methods:

1. Network TAP
2. Port mirroring

### Network TAP

A network TAP is placed inline and creates a copy of traffic for a monitoring system.

The key advantage is that the monitoring system receives a copy of the traffic without becoming the original communication endpoint.

### Port Mirroring

Port mirroring is a switch-based method that copies traffic from one interface to another monitoring interface.

The material used a Cisco SPAN example:

```text
Switch(config)# monitor session 1 source interface fastEthernet0/1
Switch(config)# monitor session 1 destination interface fastEthernet0/2
```

The exact command syntax depends on the network platform.

## Practical Scenario 1

The scenario was named **Malicious PS Download**.

The task required placing the TAP at the most efficient point to observe the HTTP traffic between the workstation and the external server.

The correct placement was:

**WP1**

After placement, the packet panel exposed an HTTP response with:

- Source: `203.0.113.200`
- Destination: `192.168.0.3`
- HTTP status: `200`
- Content type: ZIP
- Downloaded filename: `install.ps1`
- Body preview containing the flag

### Flag

`THM{FoundTheMalware}`

## Why Placement Matters

A TAP is useful only if it is positioned where the relevant traffic passes.

Poor placement can result in:

- No useful packets
- Incomplete visibility
- Excessive unrelated traffic
- Difficulty identifying the malicious session

Therefore, traffic direction and network topology must be understood before collecting evidence.

## Evidence

Primary evidence:

`Screenshots/03-scenario1-malicious-ps-download.png`

Additional exercise context:

`Screenshots/05-network-tap-exercise.png`

## Analyst Takeaway

Packet capture is most useful when the collection point is selected deliberately. Before investigating packet contents, establish which link contains the communication of interest.
