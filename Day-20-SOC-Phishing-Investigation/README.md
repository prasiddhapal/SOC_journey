# 🚨 SOC Case 020 — Phishing Investigation

> **Case Type:** Phishing & Malicious URL Investigation  
> **Severity:** 🟠 Medium  
> **Status:** 🟢 Closed  
> **Environment:** Authorized Security Lab

---

## 🎯 Executive Summary

A user received a phishing email impersonating a Windows 11
upgrade notification.

The investigation identified a suspicious sender, malicious URL,
and related network activity.

Endpoint compromise was **not confirmed** based on the available evidence.

---

## 🧩 Investigation Scenario

A user received an email claiming that a Windows 11 upgrade
was available.

The message contained a suspicious link that required investigation.

### Investigation Objectives

- Analyze the phishing email
- Identify suspicious indicators
- Investigate the URL
- Review related network activity
- Determine whether endpoint compromise occurred
- Document appropriate SOC actions

---

## 🔎 Key Findings

| Finding | Result |
|---|---|
| 📧 Phishing email | Confirmed |
| 👤 Suspicious sender | Identified |
| 🌐 Malicious URL | Identified |
| 💻 Browser access | Observed via `chrome.exe` |
| 🌐 HTTP response | `200 OK` |
| 🚨 Endpoint compromise | **Not confirmed** |

---

## 🧬 Indicators of Compromise

| Type | Indicator |
|---|---|
| Sender | `update@windows-update.site` |
| Domain | `windows-update.site` |
| URL | `https://windows-update.site/` |
| IP | `132.32.40.201` |

> ⚠️ Indicators shown here belong to an authorized security lab.

---

## 🛰️ Investigation Flow

```text
Phishing Email
      ↓
Sender Analysis
      ↓
URL Extraction
      ↓
Domain Investigation
      ↓
Network Activity Review
      ↓
IOC Extraction
      ↓
Endpoint Assessment
      ↓
SOC Decision
