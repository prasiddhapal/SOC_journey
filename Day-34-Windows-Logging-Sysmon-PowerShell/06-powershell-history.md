# Module 06 | PowerShell Logging

Sysmon can show `powershell.exe` starting but does not necessarily expose every command executed inside the session.

## History location
`C:\Users\<USER>\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt`

The file records commands entered into PowerShell. It does not record command output or automatically expose script contents.

## Manual workflow
1. Open the user's PSReadLine directory.
2. Open `ConsoleHost_history.txt`.
3. Read commands in order.
4. Open file Properties.
5. Record creation timestamp.
6. Check other users when appropriate.

## Lab findings
First command:
`Get-ComputerInfo`

History file creation date:
`May 18, 2025`

Exact creation time observed:
`8:49:26 PM`

Flag command:
`echo "THM{it_was_me!}" > flag.txt`

Flag:
`THM{it_was_me!}`

## Other observed commands
`Get-Content`
`Get-LocalUser`
`Get-LocalGroup`
`Get-DnsClientServerAddress`
`ping google.com`
`Get-Service`
`Set-ItemProperty`
`Stop-Service`

## Lesson
PowerShell history can expose discovery, file access, network testing, service manipulation and other command-level activity that process creation alone misses.
