# Windows Event Viewer

## Objective

Learn how to navigate Windows Event Viewer and identify security-relevant telemetry for SOC investigations.

## Event Viewer Structure

```text
Event Viewer
├── Windows Logs
│   ├── Application
│   ├── Security
│   ├── Setup
│   └── System
│
└── Applications and Services Logs
```

## Security Log

The **Security** log was used during the practical investigation.

It contains security auditing events such as:

- Authentication
- Process creation
- Object access
- Handle activity

## Filtering Events

Use:

```text
Security
  ↓
Filter Current Log
  ↓
Event ID
  ↓
Open Event
  ↓
Details
```

Filtering by Event ID makes it easier to investigate a specific type of activity.

## Important Events Investigated

| Event ID | Activity |
|---|---|
| 4624 | Successful logon |
| 4658 | Object handle closed |
| 4688 | Process creation |
| 4690 | Handle duplication |
| 4104 | PowerShell Script Block Logging |

## Event Details

When investigating an event, review:

- Event ID
- Time Created
- User / Account
- Computer
- Process
- PID
- PPID
- Command Line
- Logon ID
- Event Record ID

The available fields depend on the event and logging configuration.

## Friendly View vs XML

### Friendly View

Useful for quickly understanding the event and locating important fields.

### XML View

Useful when more detailed or structured telemetry is required.

Example:

```text
Event
├── System
│   ├── Provider
│   ├── EventID
│   ├── Level
│   ├── TimeCreated
│   └── Computer
│
└── EventData
    ├── User
    ├── Process
    ├── PID
    └── CommandLine
```

## Practical Investigation

During the lab, Event Viewer was used to investigate:

```text
4658 → Handle activity
4688 → Process creation
4624 → Successful logon
4690 → Handle duplication
```

PowerShell Operational logging was also checked for:

```text
4104 → PowerShell Script Block Logging
```

Event ID `4104` was not available in the training VM.

## Investigation Workflow

```text
Open Event Viewer
      ↓
Select Relevant Log
      ↓
Filter Event ID
      ↓
Inspect Event Details
      ↓
Extract Telemetry
      ↓
Correlate Related Events
      ↓
Build Timeline
      ↓
Investigate Further
```

## Key Lesson

> **Event Viewer provides telemetry. The analyst must correlate that telemetry before reaching a security verdict.**

## Status

**Completed ✅**
