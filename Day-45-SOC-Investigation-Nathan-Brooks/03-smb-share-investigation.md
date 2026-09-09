# 03 - SMB Share Investigation

## Destination
- Host: `THM-SHR-SRV`
- Share: `\\*\\Marketing`
- User: `nathan.brooks`
- Source: `10.5.50.12`

## Key Event
Windows EventCode `5145` recorded access to:

`nathan brooks notes.txt`

The critical operation occurred at approximately:

`2026-02-03 21:20:14`

Access:

`WriteData (or AddFile)`

## Additional Activity
The file was associated with multiple SMB operations, including:
- `READ_CONTROL`
- `ReadAttributes`
- `SYNCHRONIZE`
- `WriteData (or AddFile)`
- later `DELETE`

## Assessment
The logs confirm network-share file manipulation. They do not independently establish whether the activity was authorized business activity, accidental activity, or malicious behavior.
