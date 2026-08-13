# Investigation

## Initial Authentication

Event ID 4624 recorded a successful network logon.

- User: Administrator
- Logon Type: 3
- Source IP: 10.49.108.37
- Action: successful_logon

## Process Creation

Event ID 4688 recorded two process creation events.

### PowerShell

- Process: powershell.exe
- Parent: explorer.exe
- PID: 4216
- Command: powershell.exe -NoProfile

### Command Prompt

- Process: cmd.exe
- Parent: powershell.exe
- PID: 4332
- Command: cmd.exe /c whoami

## Correlation

The events form the following sequence:

4624
Successful network logon
        |
        v
Administrator
        |
        v
PowerShell
        |
        v
cmd.exe /c whoami

## Assessment

The sequence is suspicious because an Administrator network
logon was followed shortly by PowerShell and command execution.

However, this evidence does not independently prove malicious
activity.

The source IP and account activity require additional validation.
