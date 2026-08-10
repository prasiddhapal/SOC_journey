# Phishing Investigation

## Email Analysis

**Sender:** `update@windows-update.site`  
**Recipient:** `dylan@letsdefend.io`  
**Subject:** `Upgrade your system to Windows 11 Pro for FREE`

The email used a fake Windows upgrade theme to persuade the recipient to access the provided link.

## URL Analysis

```text
https://windows-update.site/

The landing page displayed a fake Windows 11 Pro upgrade page and suspicious verification instructions.

Access Evidence

The HTTP log showed:

URL: windows-update.site
Referrer: mail.letsdefend.io
Process: chrome.exe
HTTP Status: 200 OK

This confirms access to the phishing URL.

Investigation Limitation

Endpoint execution and full compromise could not be confirmed because the available telemetry was incomplete.

Conclusion

The evidence supports a phishing incident with confirmed URL access.

Malware execution, credential theft, and persistence remain unconfirmed.
