# 01 | Kerberos & Authentication

4768 = Kerberos Authentication Service/TGT request.
4769 = Kerberos service-ticket/TGS request.
4771 = Kerberos pre-authentication failure.
4776 = NTLM credential validation.

Kerberos flow:
User -> DC/KDC -> TGT -> TGS -> Target service.

The investigation emphasized failure/success correlation and source-host context rather than treating any single event as proof of compromise.
