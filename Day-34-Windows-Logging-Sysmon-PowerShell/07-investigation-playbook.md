# Module 07 | Windows Endpoint Investigation Playbook

## Phase 1: Initial access
Start with:
`4625 -> failed logons`
`4624 -> successful logon`

Check source IP, username, Logon Type, timestamp and Logon ID.

## Phase 2: Persistence
Search:
`4720`
`4732`
`4738`

Ask:
- Was a new account created?
- Who created it?
- Which groups was it added to?
- Does the Logon ID match the suspicious login?

## Phase 3: Process execution
Use Sysmon Event ID 1.

Check:
- Image
- Process ID
- Parent Process ID
- Command line
- User
- Logon ID
- Hash

## Phase 4: Files
Use Sysmon Event ID 11.
Look for Startup, Temp, Public, scripts and executables.

## Phase 5: Network
Use Sysmon Event ID 3 and 22.
Check destination IP, port, protocol, query name, query result and Process ID.

## Phase 6: PowerShell
Review `ConsoleHost_history.txt` for each relevant user.

## Correlation rules
`4624.LogonID == 4720.LogonID`
`Sysmon1.ProcessId == Sysmon3/11/22.ProcessId`
`Child.ParentProcessId == Parent.ProcessId`

## Lab timeline
1. RDP brute force
2. Successful Administrator RDP login
3. `svc_sysrestore` created
4. Backdoor account added to privileged groups
5. Chrome downloaded `ckjg.exe`
6. `ckjg.exe` created Startup persistence
7. `ckjg.exe` connected to external C2
8. PowerShell history revealed additional commands

## Core lesson
The strongest evidence came from correlation:
Event ID + timestamp + Logon ID + Process ID + user + IP.
