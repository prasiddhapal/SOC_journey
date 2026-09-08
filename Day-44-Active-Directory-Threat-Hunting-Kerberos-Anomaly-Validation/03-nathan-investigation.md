# 03 | Nathan Investigation

Query:
```spl
index=win EventCode=4769 Account_Name="nathan.brooks@*"
| table _time, Account_Name, Service_Name, Client_Address, Ticket_Encryption_Type
| sort _time
```

Observed:
- 8 TGS events
- Source: `::ffff:10.5.50.12`
- Services included `THM-DC$`, `THM-MKT-WS$`, `krbtgt`, and `THM-SHR-SRV$`
- Encryption observed: `0x12`

The Marketing workstation service was consistent with the onboarding context established on Day 43.
