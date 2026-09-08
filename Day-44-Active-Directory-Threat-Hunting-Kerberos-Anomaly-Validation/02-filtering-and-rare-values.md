# 02 | Filtering and Rare Values

Filter:
```spl
index=win EventCode=4769
| where NOT match(Account_Name, "\$@")
| stats count by Account_Name, Service_Name, Ticket_Encryption_Type
| sort - count
```

Result: 29 non-computer-account events.

Rare-pair hunt:
```spl
index=win EventCode=4769
| where NOT match(Account_Name, "\$@")
| stats count by Account_Name, Service_Name
| where count <= 1
| sort Account_Name, Service_Name
```

Result: 13 one-time account/service pairs.

Rare values were treated as leads, not conclusions.
