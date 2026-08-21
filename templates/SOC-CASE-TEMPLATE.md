🧮 Detection Logic

The lab detection identifies suspicious PowerShell
command patterns including:

EncodedCommand
-enc
ExecutionPolicy
download
iex

Parent processes such as:

winword.exe
excel.exe
outlook.exe

increase the contextual risk.

The scoring model used:

risk_score =
    (suspicious × 2)
    +
    (parent_risk × 3)
🧪 Validation Results
Negative Test
explorer.exe
    ↓
powershell.exe -NoProfile

Result:

suspicious    = 0
parent_risk   = 0
risk_score    = 0
severity      = Low

Result: PASS

Positive Test
winword.exe
    ↓
powershell.exe -EncodedCommand ABC123

Result:

suspicious    = 1
parent_risk   = 1
risk_score    = 5
severity      = High

Result: PASS

🛡️ SOC Actions
Action	Purpose
Process baseline	Establish normal behavior
Command analysis	Identify suspicious PowerShell
Parent enrichment	Add execution context
Risk scoring	Prioritize events
Positive validation	Confirm detection
Negative validation	Test false-positive behavior
🧠 Analyst Assessment
Confirmed
PowerShell behavior can be evaluated from command data.
Parent process context improves detection confidence.
Office-launched PowerShell received elevated risk.
Benign Explorer-launched PowerShell remained Low risk.
The detection produced explainable output.
Not Confirmed
No real-world compromise was established.
No external malicious infrastructure was identified.
No production incident was investigated.
Analyst Principle

Detection should evaluate behavior in context rather
than relying on a single suspicious indicator.

📋 Recommended Response

For a production alert matching this behavior:

Review the PowerShell command line.
Investigate the parent process.
Identify the initiating user.
Review related process activity.
Correlate surrounding authentication and network
events.
Escalate when additional malicious indicators exist.
📚 Investigation Evidence
🔎 Evidence 01 — PowerShell Baseline

Normal PowerShell execution was established using
explorer.exe as the parent process.

🔎 Evidence 02 — Suspicious Command Analysis

The encoded PowerShell command matched the configured
suspicious command indicators.

🔎 Evidence 03 — Parent Process Context

winword.exe was identified as a higher-risk parent
process.

🔎 Evidence 04 — Risk Score Calculation

The suspicious command and Office parent produced:

risk_score = 5
🔎 Evidence 05 — Benign Context Validation

Normal PowerShell activity produced:

risk_score = 0
severity = Low
🔎 Evidence 06 — Suspicious Context Validation

The controlled suspicious event produced:

risk_score = 5
severity = High
🔎 Evidence 07 — Final Context-Aware Detection

The final detection produced an explainable result
containing behavior, parent context, risk score,
severity, and reason.

💡 Key Lesson

Detection engineering becomes more useful when events
are evaluated using multiple contextual signals.

The Day 28 implementation progressed from simple
PowerShell matching toward context-aware risk scoring.

✅ Case Status

INVESTIGATION COMPLETE

Case:       DAY-28-SPLUNK-CONTEXT
Category:   Detection Engineering
Technique:  PowerShell / Process Context
Validation: Positive + Negative
Result:     LAB VALIDATED
📈 SOC Journey
Day 20 ─ SOC Phishing Investigation
   ↓
Day 21 ─ Alert Triage / Network Investigation
   ↓
Day 22 ─ Windows Event Investigation
   ↓
Day 23 ─ Splunk Investigation
   ↓
Day 24 ─ Splunk Detection
   ↓
Day 25 ─ Transaction Analysis
   ↓
Day 26 ─ Authentication Hunting
   ↓
Day 27 ─ Detection Engineering
   ↓
Day 28 ─ Context-Aware Detection
Current Goal

Build from:

Investigation
     ↓
Detection
     ↓
Validation
     ↓
Context Enrichment
     ↓
Risk Scoring
     ↓
Explainable SOC Detection


### One important fix


Your original template says **"Indicators of Compromise"**. For Day 28, I'd change that to **"Indicators of Interest"** because these were controlled lab values and you did **not** establish an actual compromise. That's a small distinction, but good SOC documentation is annoyingly particular about such things, for once with good reason.
