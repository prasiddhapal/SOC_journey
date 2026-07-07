# Practical Notes

## Network Interface Analysis

### Observation

- Identified Loopback, Wireless and Docker network interfaces.
- Observed assigned private IPv4 and IPv6 addresses.

### Key Learning

- Different interfaces serve different networking purposes.
- Loopback communication remains inside the local system.

### SOC Relevance

Understanding active interfaces helps analysts identify where network communication originates.

---

## Routing Table Analysis

### Observation

- Identified the default gateway.
- Observed routes for local and Docker networks.

### Key Learning

- The routing table determines where packets are forwarded.

### SOC Relevance

Routing information assists analysts when investigating suspicious outbound communication.

---

## Connectivity Testing

### Observation

- Successfully reached an external host with zero packet loss.

### Key Learning

- Successful connectivity confirms basic network communication.

### SOC Relevance

Connectivity testing helps distinguish network issues from service or application problems.

---

## DNS Resolution

### Observation

- Successfully resolved a domain into IPv4 and IPv6 addresses.
- Observed the configured DNS server.

### Key Learning

- DNS translates domain names into IP addresses before communication begins.

### SOC Relevance

DNS investigations help analysts understand where systems are attempting to communicate.
