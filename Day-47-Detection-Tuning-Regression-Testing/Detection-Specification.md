# Detection Specification

## Name
Office Application → Suspicious PowerShell

## Objective
Detect suspicious PowerShell execution originating from Microsoft Office applications while minimizing predictable administrative false positives.

## Required telemetry
- Parent process image
- Child process image
- Command line
- Host
- User
- Process ID
- Timestamp

## Base logic
```text
Office parent
AND
PowerShell child
AND
(
  EncodedCommand
  OR HiddenWindow
)
```

## Suspicious command-line patterns
- `-enc`
- `-EncodedCommand`
- `-WindowStyle Hidden`
- `-w hidden`

## Weak signal not used alone
- `-NoProfile`

## Correlation layer
Network activity may increase confidence when the same process makes an external connection.

## Severity
High for the tested suspicious behavior chain.

## Response
Alert and investigate first. Automatic containment requires additional evidence and organizational authorization.

## False-positive considerations
- Approved Office add-ins
- Helpdesk automation
- Enterprise administrative scripts
- Software deployment/management

## Exclusion principle
Prefer contextual controls such as signed publisher/path, documented automation, known service account, and approved workflow. Avoid brittle command-line-hash exclusions.
