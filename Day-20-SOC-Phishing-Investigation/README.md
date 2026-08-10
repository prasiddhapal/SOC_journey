# Day 20 - SOC Phishing Investigation

## Objective

Investigated a phishing email and analyzed related URL and network activity.

## Scenario

A user received a fake Windows 11 Pro upgrade email containing a suspicious link.

## Key Findings

- Phishing email delivered to the user
- Suspicious sender domain identified
- Malicious URL identified
- URL access observed through `chrome.exe`
- HTTP response: `200 OK`
- Endpoint compromise not confirmed

## IOCs

- **Sender:** `update@windows-update.site`
- **Domain:** `windows-update.site`
- **URL:** `https://windows-update.site/`
- **IP:** `132.232.40.201`

## SOC Actions

- Analyze email and URL
- Extract IOCs
- Correlate logs
- Assess severity
- Recommend containment

## Key Lesson

**Do not claim compromise without sufficient evidence.**

## Status

**Day 20 - Completed ✅**
