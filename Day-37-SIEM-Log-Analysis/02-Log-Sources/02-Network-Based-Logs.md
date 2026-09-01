# 02 - Network-Based Log Sources

## Overview

Network-based logs originate from infrastructure that observes communications.

## Common Sources

- Firewalls
- IDS/IPS
- Routers
- VPN systems
- DNS systems
- Proxy servers

## Firewall Logs

Firewalls can show connections between internal and external systems.

Useful fields may include:

- Source IP
- Destination IP
- Source port
- Destination port
- Action
- Timestamp

## IDS/IPS

IDS and IPS systems can identify suspicious traffic patterns.

## Router Logs

Router telemetry can provide visibility into network activity and infrastructure events.

## VPN Logs

VPN logs can help identify remote access and authentication activity.

## DNS Logs

DNS activity can provide visibility into hostname resolution.

## Proxy Logs

Proxy logs can provide visibility into web-related outbound traffic.

## Detection Examples

### Port Scanning

Repeated attempts across multiple ports may indicate scanning.

### Suspicious External Connections

Unexpected connections to external systems may require investigation.

### Brute Force

Repeated authentication attempts may be correlated with authentication logs.

## Analyst Perspective

Network logs answer:

"How did systems communicate?"

They are especially useful when correlated with host and identity telemetry.
