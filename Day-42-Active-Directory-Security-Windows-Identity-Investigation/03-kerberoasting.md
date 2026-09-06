# 03 | Kerberoasting Concepts

SPNs associate services with accounts, for example:

MSSQLSvc/sql01.corp.local:1433
HTTP/web01.corp.local

Conceptual chain:

SPN → service account → TGS request → offline cracking → possible credential recovery.

Potential signals:
- unusual TGS volume
- multiple SPN/service-account requests
- unusual source host
- RC4/legacy encryption
- privileged service accounts

Important: one 4769 event or RC4 ticket does not confirm Kerberoasting.
