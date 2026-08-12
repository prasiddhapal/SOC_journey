# PowerShell Logging

## Objective

Understand how PowerShell Script Block Logging can provide visibility into PowerShell activity during a SOC investigation.

## Event ID 4104

Event ID `4104` is associated with **PowerShell Script Block Logging**.

It can provide script content that helps an analyst understand what PowerShell attempted to execute.

## Expected Location

```text
Applications and Services Logs
└── Microsoft
    └── Windows
        └── PowerShell
            └── Operational
```

## Investigation Workflow

```text
PowerShell Activity
      ↓
PowerShell Operational Log
      ↓
Event ID 4104
      ↓
Script Block Content
      ↓
Analyze Command
      ↓
Correlate Endpoint / Network Activity
      ↓
Determine Verdict
```

## Practical Investigation

The PowerShell Operational log was checked for Event ID `4104`.

### Result

Event ID `4104` was **not available in the training VM**.

Therefore:

- PowerShell Script Block content could not be reviewed.
- No conclusion was made from missing script telemetry.
- The telemetry limitation was documented.

## What Additional Evidence Would Help?

If 4104 were available, correlate the script with:

- Event ID 4688
- PowerShell process information
- Command line
- File creation
- Network connections
- DNS activity
- User and Logon ID
- Timeline

## AI-Assisted Investigation

AI can help analyze PowerShell commands and identify possible behaviors, but the analyst must validate the findings against actual telemetry.

```text
AI Analysis
    ↓
Hypothesis
    ↓
Available Telemetry
    ↓
Analyst Validation
    ↓
Conclusion
```

## Key Lesson

> **Missing telemetry is a documented limitation, not evidence that an activity did or did not occur.**

## Status

**Completed with telemetry limitation ⚠️**
