# Linux Network Analysis for SOC Analysts

## 📖 Introduction

Network analysis is a core responsibility of a Security Operations Center (SOC) analyst. Investigating active connections, listening services, HTTP responses, and DNS records helps identify suspicious communication, unauthorized services, and potential security threats.

---

## 🎯 Learning Objectives

- Analyze active network connections
- Identify listening ports
- Understand socket statistics
- Compare `ss` and `netstat`
- Inspect HTTP response headers
- Perform advanced DNS lookups
- Apply networking commands during SOC investigations

---

## 📚 Topics Covered

### Network Connections

- ss
- Socket Statistics
- Connection States
- Listening Ports

### Network Monitoring

- netstat
- Active Connections

### HTTP Analysis

- curl
- HTTP Response Headers
- HTTP Status Code 301

### DNS Analysis

- dig
- DNS A Record
- TTL
- DNS Query Information

---

## 🛡️ Practical Investigation

During this lab the following investigations were performed:

- Enumerated listening TCP and UDP ports.
- Identified active network connections.
- Compared `ss` and `netstat` outputs.
- Retrieved HTTP response headers from a web server.
- Observed HTTP redirection behavior.
- Investigated DNS records using `dig`.

---

## 📂 Documentation

- Commands → commands.md
- Notes → notes.md
- Interview Questions → interview_questions.md

---

## 📸 Screenshots

- Socket Statistics Analysis
- Network Connection Analysis
- HTTP Header Analysis
- DNS Record Analysis

---

## 🎯 Key Takeaways

- `ss` is the preferred modern utility for socket analysis.
- Listening ports should always be verified against expected services.
- HTTP headers provide valuable information during web investigations.
- DNS records help map domains to IP addresses.
- Multiple sources of evidence should always be correlated before reaching a security conclusion.
