# 🪟 SOC Case 022 — Windows Event Investigation

> **Case Type:** Windows Event & Endpoint Investigation  
> **Severity:** 🟠 Medium  
> **Status:** 🟢 Investigation Complete  
> **Environment:** Authorized Security Lab  
> **Focus:** Windows Security Logs · Process Creation · Authentication · PowerShell

---

## 🎯 Executive Summary

This investigation focused on analyzing Windows event telemetry and correlating authentication, process, and PowerShell activity.

The investigation examined Windows Security events including successful logons, process creation, and PowerShell Script Block Logging.

Rather than treating individual events as isolated findings, the investigation correlated:

**User → Logon → Process → Parent Process → Command Line → PowerShell → Timestamp**

> **Analyst Principle:** A single Windows event rarely provides enough context to determine malicious activity. Correlation creates the investigation story.

---

## 🧩 Investigation Scenario

A Windows endpoint generated multiple security-relevant events requiring investigation.

The objective was to determine:

- Which user authenticated?
- When did the authentication occur?
- Which process was created?
- Which parent process launched it?
- What command line was executed?
- Was PowerShell involved?
- Could the events be correlated into a meaningful activity sequence?

---

## 🔎 Investigation Objectives

- Analyze Windows Security event telemetry.
- Investigate successful authentication events.
- Analyze process creation events.
- Correlate PID and PPID relationships.
- Investigate PowerShell Script Block Logging.
- Correlate events using timestamps and user context.
- Identify missing or incomplete telemetry.
- Build an evidence-based analyst assessment.

---

## 📊 Key Findings

| Finding | Event / Evidence | Result |
|---|---|---|
| Successful authentication | Event ID 4624 | Investigated |
| Process creation | Event ID 4688 | Investigated |
| Process relationship | PID / PPID | Correlated |
| Command-line activity | Process telemetry | Analyzed |
| PowerShell activity | Event ID 4104 | Investigated |
| Event correlation | Multiple telemetry sources | Performed |
| Missing telemetry | PowerShell logging | Identified |

---

## 🛰️ Investigation Flow

```text
Windows Security Event
        ↓
Authentication Analysis
        ↓
Process Creation
        ↓
PID / PPID Correlation
        ↓
Command-Line Analysis
        ↓
PowerShell Telemetry
        ↓
Timestamp Correlation
        ↓
Analyst Assessment
        ↓
Response Recommendation
🔐 Authentication Investigation
Event ID 4624 — Successful Logon

Event ID 4624 was reviewed to identify successful authentication activity.

Investigation fields included:

Account / username
Logon type
Source information
Timestamp
Authentication context
Associated host
Authentication Questions
Who authenticated?
      ↓
When?
      ↓
From where?
      ↓
Using which logon type?
      ↓
What happened after authentication?

A successful logon is not inherently malicious. Authentication must be evaluated against user, host, time, source, and subsequent activity.

⚙️ Process Investigation
Event ID 4688 — Process Creation

Process creation telemetry was examined to identify processes launched on the endpoint.

Relevant fields included:

New process
Process ID
Parent Process ID
Command line
Account
Timestamp
Process Relationship
Parent Process
      ↓
PID / PPID
      ↓
Child Process
      ↓
Command Line
      ↓
Behavior

This relationship helps determine whether process execution is consistent with expected endpoint behavior.

⚡ PowerShell Investigation

PowerShell activity was investigated using available Windows telemetry.

Event ID 4104 — Script Block Logging

PowerShell Script Block Logging can provide visibility into PowerShell commands and script content.

The investigation considered:

PowerShell execution
Script content
Command behavior
User context
Parent process
Timestamp correlation
Important Telemetry Limitation

Missing or incomplete PowerShell logging reduces visibility into PowerShell-based activity.

This is itself an important SOC finding because:

No telemetry does not mean no activity.

🔗 Event Correlation

The investigation correlated multiple events rather than relying on a single event ID.

Correlation Model
4624
Successful Logon
      │
      ▼
User Context
      │
      ▼
4688
Process Creation
      │
      ▼
PID / PPID
      │
      ▼
Command Line
      │
      ▼
4104
PowerShell Activity
      │
      ▼
Analyst Assessment
Correlation Fields
Field	Purpose
Timestamp	Establish event sequence
User	Identify account involved
Host	Identify affected endpoint
PID	Identify process
PPID	Identify parent process
Command Line	Understand execution
Event ID	Identify event type
🧬 Indicators of Interest
Type	Value	Relevance
User	[Observed account]	Authentication context
Host	[Observed host]	Endpoint context
Process	[Observed process]	Execution context
PID	[Observed PID]	Process correlation
PPID	[Observed PPID]	Parent-process correlation
Command	[Observed command]	Execution behavior

⚠️ Populate these values from the actual investigation evidence. Do not invent indicators.

🧠 Analyst Assessment
Confirmed
Windows authentication telemetry was analyzed.
Process creation telemetry was investigated.
PID and PPID relationships were examined.
Event timestamps were correlated.
PowerShell telemetry was reviewed where available.
Suspicious / Requires Further Investigation
[Insert suspicious behavior supported by evidence]
[Insert additional finding if applicable]
Not Confirmed
No unsupported conclusion of compromise was made.
[Insert activity that could not be established]

Analyst Principle: Event IDs provide evidence, not conclusions. Context determines significance.

🛡️ SOC Actions
Action	Purpose
Review Event ID 4624	Establish authentication context
Review Event ID 4688	Identify process execution
Correlate PID / PPID	Establish process relationships
Review Event ID 4104	Investigate PowerShell activity
Correlate timestamps	Establish event sequence
Review user and host context	Determine whether behavior is expected
Identify telemetry gaps	Improve detection visibility
📋 Recommended Response

For a production investigation involving similar Windows activity:

Identify the affected host.
Identify the user associated with the activity.
Review successful and failed authentication events.
Investigate process creation events.
Correlate PID and PPID relationships.
Review command-line activity.
Investigate PowerShell telemetry where available.
Correlate endpoint activity with network and authentication logs.
Escalate when additional indicators support malicious activity.
Document telemetry gaps that could affect detection.
📚 Investigation Evidence
🔎 Evidence 01 — Windows Security Log

[Describe the Windows Security event and relevant fields.]

🔎 Evidence 02 — Event 4688 Process Creation

[Describe the process creation event, PID, PPID, and command-line information.]

🔎 Evidence 03 — Event 4624 Authentication

[Describe the successful authentication event and associated user/logon context.]

🧭 Evidence Chain
🔐 Authentication
      ↓
👤 User Context
      ↓
⚙️ Process Creation
      ↓
🌳 Parent / Child Relationship
      ↓
⌨️ Command Line
      ↓
⚡ PowerShell Telemetry
      ↓
🔗 Event Correlation
      ↓
🧠 Analyst Decision
📈 Investigation Timeline
Stage	Event	Analyst Action	Result
01	Authentication	Reviewed Event 4624	[Result]
02	Process Creation	Reviewed Event 4688	[Result]
03	Process Context	Correlated PID / PPID	[Result]
04	PowerShell	Reviewed Event 4104	[Result]
05	Correlation	Compared timestamps and context	[Result]
06	Assessment	Evaluated evidence	[Result]
💡 Key Lessons
01 — Correlation Beats Isolation

A single event rarely tells the complete story.

02 — PID / PPID Context Matters

Process relationships can reveal how execution originated.

03 — Authentication Provides Context

User and logon information helps determine whether subsequent activity is expected.

04 — Telemetry Gaps Matter

Missing PowerShell or command-line telemetry can reduce investigation confidence.

05 — Evidence Before Conclusions

SOC analysts should distinguish between:

Observed → Correlated → Suspected → Confirmed

🔐 Ethics & Lab Scope

This investigation was conducted in an authorized security training environment for educational and defensive security purposes.

No unauthorized systems, accounts, infrastructure, or data were targeted.

✅ Case Status

🟢 INVESTIGATION COMPLETE

