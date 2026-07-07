# Linux Networking for SOC Analysts

## 📖 Introduction

Networking is a fundamental skill for Security Operations Center (SOC) analysts. Understanding how systems communicate over a network enables analysts to investigate suspicious connections, authentication attempts, routing behavior, and DNS activity during security incidents.

---

## 🎯 Learning Objectives

- Analyze Linux network interfaces
- Identify IPv4 and IPv6 addresses
- Understand private and public IP addressing
- Analyze routing tables and default gateways
- Verify network connectivity
- Investigate DNS resolution
- Apply networking concepts during SOC investigations

---

## 📚 Topics Covered

### Network Fundamentals

- IP Address
- IPv4 & IPv6
- Public vs Private IP Address

### Network Interfaces

- Loopback Interface (lo)
- Wireless Interface (wlan0)
- Docker Network (docker0)

### Routing

- Routing Table
- Default Gateway

### Connectivity

- ping

### DNS

- DNS Resolution
- nslookup
- DNS Port 53

---

## 🛡️ Practical Investigation

During this lab the following investigations were performed:

- Examined local network interfaces.
- Identified private IPv4 and IPv6 addresses.
- Investigated routing table entries.
- Identified the system's default gateway.
- Verified external network connectivity.
- Resolved a domain name into IPv4 and IPv6 addresses.
- Observed DNS server responses.

---

## 📂 Documentation

- Commands → commands.md
- Notes → notes.md
- Interview Questions → interview_questions.md

---

## 📸 Screenshots

- Network Interface Analysis
- Routing Table Analysis
- Connectivity Test
- DNS Resolution Analysis

---

## 🎯 Key Takeaways

- Linux networking begins with understanding interfaces and IP addressing.
- Routing tables determine how packets reach external networks.
- DNS translates domain names into IP addresses.
- Connectivity testing is an important troubleshooting step before drawing conclusions during investigations.
- Network evidence should always be correlated with logs and system activity before reaching a conclusion.
