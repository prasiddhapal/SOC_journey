# 02 | Kerberos Authentication

```text
User
 ↓
KDC / Domain Controller
 ↓
4768 → TGT
 ↓
4769 → TGS for a specific service
 ↓
Target service
```

TGT: ticket used by the client to obtain service tickets from the KDC.

TGS/service ticket: ticket issued for a specific service.

Neither 4768 nor 4769 is inherently malicious. Analysts assess account, source host, service, time, frequency, encryption and surrounding endpoint telemetry.
