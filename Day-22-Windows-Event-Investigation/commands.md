# Day 22 - Windows Investigation Commands

## Event Viewer

Open Windows Event Viewer:

```cmd
eventvwr.msc
```

Useful for manually reviewing Windows event logs.

## PowerShell Process Investigation

List running processes:

```powershell
Get-Process
```

Get detailed process information:

```powershell
Get-CimInstance Win32_Process
```

Find a specific process:

```powershell
Get-Process -Name powershell
```

## Network Investigation

Show active network connections:

```cmd
netstat -ano
```

PowerShell alternative:

```powershell
Get-NetTCPConnection
```

The `-ano` output can be correlated with a PID to identify the process associated with a network connection.

## Process Investigation

List processes:

```cmd
tasklist
```

Display processes and associated services:

```cmd
tasklist /svc
```

## Event Log Investigation

PowerShell can query Windows event logs with:

```powershell
Get-WinEvent -LogName Security
```

Query a specific Event ID:

```powershell
Get-WinEvent -FilterHashtable @{
    LogName = 'Security'
    Id = 4688
}
```

Query successful logons:

```powershell
Get-WinEvent -FilterHashtable @{
    LogName = 'Security'
    Id = 4624
}
```

## Investigation Workflow

```text
Event Log
   ↓
Event ID
   ↓
Process / User
   ↓
PID / PPID
   ↓
Network Connection
   ↓
Timeline
   ↓
Correlation
```

## Key Lesson

Commands provide supporting telemetry.

Always correlate command output with:

- Event logs
- Process IDs
- Users
- Timestamps
- Network activity
- File activity

## Status

**Completed ✅**
