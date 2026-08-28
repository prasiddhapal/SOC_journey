# Module 04 | Sysmon: Process Monitoring

Sysmon Event ID 1 provides detailed process creation telemetry.

Location:
`Applications and Services -> Microsoft -> Windows -> Sysmon -> Operational`

## Event ID 1 fields
### Process
- Process ID
- Image
- Command line

### Parent
- Parent Process ID
- Parent image
- Parent command line

### Binary
- Hash
- Signature
- PE metadata

### User
- User
- Logon ID

## Investigation workflow
1. Filter Event ID 1.
2. Review executable path.
3. Check process name.
4. Inspect parent.
5. Compare Process ID and Parent Process ID.
6. Review hash when available.
7. Correlate Logon ID.

## Lab findings
- Browser: `Google Chrome`
- Downloaded file: `C:\Users\sarah.miller\Downloads\ckjg.exe`
- Download URL: `http://getsvr1ff.com/bgj3/ckjg.exe`

## Investigation chain
Sarah -> Chrome -> ckjg.exe -> file/network/DNS activity

## Lesson
Use path + parent + command line + hash + user + Logon ID + follow-on activity rather than relying on a filename alone.
