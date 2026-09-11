# Detection Specification

## Detection Name

Microsoft Office Spawning Suspicious PowerShell

## Objective

Identify Microsoft Word or Excel spawning PowerShell or PowerShell Core with suspicious encoded-command or hidden-window execution characteristics.

## Log Source

```yaml
product: windows
category: process_creation
```

## Parent Processes

```text
WINWORD.EXE
EXCEL.EXE
```

## Child Processes

```text
powershell.exe
pwsh.exe
```

## Suspicious Characteristics

```text
-enc
-EncodedCommand
-WindowStyle Hidden
-w hidden
```

## Logic

```text
Office parent
AND
PowerShell child
AND
suspicious command-line characteristic
```

## False-Positive Considerations

- Approved enterprise Office automation
- Authorized administrative scripts
- Helpdesk troubleshooting

These are documented as investigation considerations rather than blanket exclusions.

## Severity

`high`

The severity reflects the lab detection design and should be baselined against real organizational telemetry before production deployment.

## ATT&CK

Primary technique:

```text
T1059.001 - PowerShell
```
