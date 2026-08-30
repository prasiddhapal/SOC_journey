# 02 | Network Sources and Flows

## Objective

Understand where network telemetry originates and how traffic can be categorized for monitoring.

## Traffic Sources

### Endpoint Sources

Endpoint devices generate the majority of normal network traffic. Examples include:

- Hosts
- Servers
- IoT devices
- Printers
- Cloud resources
- Mobile devices

### Intermediary Sources

Intermediary devices carry or inspect traffic and include:

- Firewalls
- Routers
- Switches
- Web proxies
- IDS/IPS
- Wireless infrastructure

These devices also generate useful telemetry, although typically less traffic than endpoints.

## Traffic Flow Categories

### North-South Traffic

North-South traffic crosses the boundary between the internal network and external networks.

Common examples include:

- HTTPS
- DNS
- SSH
- VPN
- SMTP
- RDP

This traffic is often monitored closely because it crosses security boundaries such as firewalls.

### East-West Traffic

East-West traffic occurs within the internal environment.

Examples include:

- SMB
- Kerberos
- Internal DNS
- DHCP
- ARP
- Routing traffic
- Database replication
- Management traffic

East-West visibility is particularly important after a compromise because attackers may use internal services for lateral movement.

## Protocol Examples

### SMB with Kerberos

Before an SMB session can be established in the scenario described by the training material, the host first contacts the authentication service using **Kerberos**.

### TLS

TLS stands for:

**Transport Layer Security**

It protects communication but can also reduce the visibility available to network monitoring tools, making metadata and endpoint telemetry important complements.

## SOC Relevance

Understanding normal traffic flows helps an analyst recognize abnormal paths.

For example:

- An endpoint suddenly communicating with an unusual external destination
- An internal workstation making unexpected administrative connections
- A system producing unusual DNS volume
- Unexpected SMB activity between hosts

## Analyst Takeaway

Traffic direction and source classification provide context. A suspicious connection is easier to evaluate when the analyst understands whether it is endpoint-to-external, endpoint-to-endpoint, or infrastructure-generated traffic.
