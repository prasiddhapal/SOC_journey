# 01 | Kerberos Hunt

Initial query:
```spl
index=win EventCode=4769
| stats count by Account_Name, Service_Name, Ticket_Encryption_Type
| sort - count
```
Result: 38 events.

Top activity was dominated by expected services such as `THM-DC$`. Volume alone was not treated as malicious.
