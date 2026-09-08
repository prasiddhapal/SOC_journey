# 04 | Source Correlation

Query:
```spl
index=win
(Client_Address="*10.5.50.12*" OR Source_Network_Address="*10.5.50.12*")
| table _time, EventCode, Account_Name, user, Workstation_Name, Source_Network_Address, Service_Name, Logon_Type
| sort _time
```

Result: 76 events.

A separate search of `192.0.2.254` showed the source was shared by multiple users. Therefore it was not treated as attacker-specific infrastructure.

Key lesson: validate whether an IP uniquely identifies a host before making attribution claims.
