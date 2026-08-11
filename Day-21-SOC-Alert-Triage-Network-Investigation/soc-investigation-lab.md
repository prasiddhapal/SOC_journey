# Day 21 - SOC Investigation Lab

## Platform

**TryHackMe - SOC L1 Alert Triage**

## Lab Focus

- Alert triage
- Alert prioritisation
- True Positive / False Positive classification
- Process investigation
- Network correlation
- Alert ownership
- Investigation workflow

## Practical Workflow

```text
Prioritise Alert
      ↓
Assign Alert
      ↓
Move to In Progress
      ↓
Read Alert Details
      ↓
Check Alert Fields
      ↓
Investigate SIEM
      ↓
Make Verdict
      ↓
Escalate or Close
```

## Alert Investigation

Review:

- Alert name
- Severity
- Status
- Verdict
- User
- Host
- Process
- Network activity
- File activity
- Related events

## Practical Findings

### Double-Extension File Creation

```text
Target:
C:\Users\S.Conway\Downloads\cats2025.mp4.exe

Process:
chrome.exe

User:
S.Conway
```

The double-extension pattern is suspicious because an executable is disguised as a media file.

### Download from GitHub Repository

```text
URL:
https://github.com/facebook/react

User:
G.Chandler

Verdict:
False Positive
```

The activity was associated with legitimate developer activity.

## Investigation Principle

Do not classify an alert from its name or severity alone.

Correlate:

```text
Alert
 ↓
Endpoint
 ↓
Process
 ↓
Network
 ↓
File
 ↓
User
 ↓
Timeline
```

## Status

**Completed ✅**
