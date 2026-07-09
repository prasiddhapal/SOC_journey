# Practical Notes

## Firewall Configuration Analysis

### Observation

- Verified firewall status and default policies.
- Confirmed incoming traffic was restricted by default.

### Key Learning

- Firewall rules determine which network traffic is allowed or denied.

### SOC Relevance

Unexpected firewall rules should be investigated before making configuration changes.

---

## Firewall Rule Management

### Observation

- Created allow and deny rules.
- Examined numbered firewall rules.

### Key Learning

- Numbered rules simplify firewall rule management.

### SOC Relevance

Firewall rules should be reviewed alongside process activity and authentication logs.

---

## OpenSSH Profile Analysis

### Observation

- Identified the predefined OpenSSH application profile.

### Key Learning

- Application profiles simplify firewall configuration for common services.

### SOC Relevance

Firewall rules should match organizational security policies and approved services.

---

## Defense in Depth

### Observation

- Firewall protection alone is not sufficient against credential compromise.

### Key Learning

- Multiple security controls work together to reduce organizational risk.

### SOC Relevance

SOC analysts should correlate firewall events with authentication logs, endpoint activity, and user behavior before reaching a conclusion.
