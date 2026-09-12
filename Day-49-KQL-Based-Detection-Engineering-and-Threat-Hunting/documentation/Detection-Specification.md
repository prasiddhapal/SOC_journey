# Detection Specification \| Office → Suspicious PowerShell

## Detection Name

Microsoft Office Spawning Suspicious PowerShell

## Objective

Identify Microsoft Office applications spawning PowerShell with encoded
or hidden execution characteristics.

## Logic

``` text
Office Application
       ↓
PowerShell
       ↓
Encoded OR Hidden Execution
       ↓
Detection
```

## Parent Processes

-   `WINWORD.EXE`
-   `EXCEL.EXE`

## Child Processes

-   `powershell.exe`
-   `pwsh.exe`

## Suspicious Characteristics

-   `-enc`
-   `-EncodedCommand`
-   `-WindowStyle Hidden`
-   `-w hidden`

`-NoProfile` alone is not considered suspicious.

## KQL

``` kusto
| where InitiatingProcessFileName in~ ("WINWORD.EXE", "EXCEL.EXE")
| where FileName in~ ("powershell.exe", "pwsh.exe")
| where ProcessCommandLine contains "-enc"
    or ProcessCommandLine contains "-EncodedCommand"
    or ProcessCommandLine contains "-WindowStyle Hidden"
    or ProcessCommandLine contains "-w hidden"
```

## Correlation

Network telemetry may be correlated by: - `DeviceName` - `ProcessId` ↔
`InitiatingProcessId`

Network activity is corroborating evidence, not a requirement for the
base detection.

## False Positives

Potential legitimate cases: - Approved Office automation - Authorized
administrative scripts - Helpdesk troubleshooting - Enterprise add-ins
or automation

Production deployment requires environmental baselining and tuning.

## MITRE ATT&CK

Primary technique: **T1059.001 \| PowerShell**

Additional techniques should only be mapped when supporting telemetry
exists.
