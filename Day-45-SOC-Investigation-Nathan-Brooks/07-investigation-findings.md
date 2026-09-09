# 07 - Final Investigation Findings

## Confirmed
1. Nathan Brooks was involved in the observed authentication and resource-access activity.
2. `THM-MKT-WS` / `10.5.50.12` was the observed source for the relevant SMB activity.
3. `THM-SHR-SRV` hosted the `Marketing` share involved in the activity.
4. `nathan brooks notes.txt` was accessed through SMB.
5. EventCode `5145` recorded `WriteData (or AddFile)` against the file at approximately `21:20:14`.
6. Subsequent file operations included synchronization and deletion activity.

## Not Confirmed
1. The process responsible for the write.
2. That `Notepad.exe` PID `9048` performed the write.
3. Malicious intent.
4. Compromise of Nathan Brooks' account.

## Severity Recommendation
Based only on the evidence collected, the activity should be treated as **suspicious and requiring contextual validation**, rather than automatically escalated as confirmed malicious activity.

## Recommended Next Actions in a Real Environment
- Validate whether Nathan Brooks was authorized to use the Marketing share.
- Confirm whether the group membership change was approved.
- Obtain endpoint file telemetry such as Sysmon FileCreate/Object Access where appropriate.
- Review EDR process/file correlation if available.
- Check the file's contents and hash through approved incident-response procedures.
- Review authentication source and session context around the activity.
