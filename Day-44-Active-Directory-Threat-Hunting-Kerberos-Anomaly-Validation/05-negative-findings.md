# 05 | Negative Findings

Nathan 4771 search:
```spl
index=win EventCode=4771 "nathan.brooks"
| table _time, EventCode, Account_Name, user, Client_Address, Failure_Code, Service_Name
| sort _time
```
Result: 0 events.

Nathan 4688 search:
```spl
index=win EventCode=4688 "nathan.brooks"
| table _time, EventCode, Account_Name, user, Parent_Process_Name, New_Process_Name, Process_Command_Line
| sort _time
```
Result: 0 events.

These negative findings weakened the original credential-abuse hypothesis.
