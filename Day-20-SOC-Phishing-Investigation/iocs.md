# Indicators of Compromise (IOCs)

## Email IOC

| Type | Indicator |
|---|---|
| Sender | `update@windows-update.site` |
| Recipient | `dylan@letsdefend.io` |
| Subject | `Upgrade your system to Windows 11 Pro for FREE` |

## Network IOCs

| Type | Indicator |
|---|---|
| Domain | `windows-update.site` |
| URL | `https://windows-update.site/` |
| Sender IP | `132.232.40.201` |

## Host Indicator

| Type | Indicator |
|---|---|
| Process | `chrome.exe` |

## Evidence

The URL access log showed:

```text
URL: https://windows-update.site/
Referrer: https://mail.letsdefend.io/
Process: chrome.exe
HTTP Status: 200 OK
