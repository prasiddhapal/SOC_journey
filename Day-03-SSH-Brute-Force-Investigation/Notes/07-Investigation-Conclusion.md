# 🛡️ Investigation Conclusion

| Field | Details |
|--------|---------|
| **Author** | Prasiddha Pal |
| **Role** | SOC Analyst Trainee |
| **Case ID** | SOC-DAY03-001 |
| **Platform** | Kali Linux |
| **Status** | ✅ Closed |

---

## 🎯 Objective

Summarize the investigation and provide an evidence-based conclusion for the observed SSH authentication activity.

---

## 📋 Investigation Summary

An SSH authentication attempt was intentionally generated using a non-existent user account in a controlled Kali Linux lab. The authentication logs were analyzed to determine whether the observed activity represented a genuine security incident.

---

## 🔍 Key Findings

- SSH authentication attempt detected.
- Username **wronguser** does not exist.
- `Invalid user` event recorded.
- Multiple `Failed password` events observed.
- Source IP Address: **127.0.0.1** (Loopback Address).
- SSH daemon terminated the connection.
- No successful authentication occurred.

---

## 📊 Risk Assessment

| Category | Assessment |
|----------|------------|
| **Severity** | 🟢 Low |
| **Impact** | Minimal |
| **Likelihood** | Low |
| **Business Risk** | None (Lab Environment) |

---

## ✅ Investigation Conclusion

Based on the collected evidence, the authentication activity was determined to be **expected laboratory testing** rather than a confirmed brute-force attack.

The investigation found no indicators of:

- Unauthorized access
- Successful authentication
- Privilege escalation
- System compromise

Therefore, the event has been classified as:

> **False Positive (Expected Lab Activity)**

---

## 📌 Recommendations

- Continue monitoring SSH authentication logs.
- Investigate repeated failed logins from external IP addresses.
- Correlate authentication events before escalating incidents.
- Enable Multi-Factor Authentication (MFA) for privileged accounts where applicable.

---

## 💡 Lessons Learned

- Evidence should always support conclusions.
- Context is essential during security investigations.
- Authentication logs provide valuable forensic evidence.
- A SOC analyst should avoid assumptions and rely on log correlation.

---

**Document Version:** 1.0

**Maintained By:** Prasiddha Pal

---
⭐ Part of the **SOC Journey** by **Prasiddha Pal**
