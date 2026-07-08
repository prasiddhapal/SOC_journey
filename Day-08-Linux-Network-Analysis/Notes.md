# Practical Notes

## Socket Statistics Analysis

### Observation

- Identified listening TCP and UDP ports.
- Observed active and established connections.

### Key Learning

- `ss` provides detailed socket information and process correlation.

### SOC Relevance

Unexpected listening ports or outbound connections should always be investigated.

---

## Network Connection Analysis

### Observation

- Compared outputs from `ss` and `netstat`.
- Verified commonly used service ports.

### Key Learning

- Both commands provide similar information, but `ss` is the modern replacement.

### SOC Relevance

Network connections should be correlated with running processes during investigations.

---

## HTTP Header Analysis

### Observation

- Retrieved HTTP response headers using `curl`.
- Observed HTTP 301 redirect and server information.

### Key Learning

- HTTP headers reveal server behavior without downloading page content.

### SOC Relevance

Useful when validating suspicious URLs or investigating web infrastructure.

---

## DNS Record Analysis

### Observation

- Resolved domain names using `dig`.
- Observed DNS A record, TTL, query time, and responding DNS server.

### Key Learning

- DNS lookups provide detailed information about domain resolution.

### SOC Relevance

DNS investigations help analysts understand where systems communicate and support IOC validation.
