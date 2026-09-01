# Day 37 - SIEM & Log Analysis

> SOC Journey | Day 37 | Security Monitoring, Log Sources, Splunk & Active Directory Detection

---

## 00 - Day Overview

Day 37 focused on the practical role of a Security Information and Event Management (SIEM) platform in a SOC environment.

The work moved from understanding different log sources into practical event investigation using Splunk.

The day also introduced an Active Directory investigation involving Kerberos authentication telemetry and AS-REP Roasting detection.

The Active Directory exercise was started but intentionally remains marked **In Progress** because the required evidence still needs to be examined manually.

---

## 01 - Learning Objectives

- Understand what a SIEM provides to a SOC analyst.
- Understand why centralised log collection matters.
- Identify host-based log sources.
- Identify network-based log sources.
- Identify web-based log sources.
- Understand time-related problems in security logs.
- Understand log normalisation.
- Use Splunk to search security events.
- Investigate Linux authentication activity.
- Investigate sudo activity.
- Inspect Windows process and network telemetry.
- Understand the role of Event ID 4768.
- Understand the indicators used in the AS-REP Roasting lab.
- Build a repeatable investigation workflow.
- Document evidence professionally.

---

## 02 - Repository Structure

```text
Day-37-SIEM-Log-Analysis/
│
├── README.md
│
├── 01-SIEM-Fundamentals/
│   └── 01-SIEM-Fundamentals.md
│
├── 02-Log-Sources/
│   ├── 01-Host-Based-Logs.md
│   ├── 02-Network-Based-Logs.md
│   ├── 03-Web-Based-Logs.md
│   └── 04-Time-and-Log-Normalisation.md
│
├── 03-Splunk-Investigations/
│   ├── 01-Splunk-Workflow.md
│   ├── 02-Linux-Authentication.md
│   ├── 03-Sudo-Investigation.md
│   └── 04-Windows-Event-Investigation.md
│
├── 04-Windows-Security-Logs/
│   └── 01-Windows-Security-Events.md
│
├── 05-Linux-Authentication/
│   └── 01-Linux-Auth-Logs.md
│
├── 06-Active-Directory-ASREP/
│   └── 01-ASREP-Roasting-Investigation.md
│
├── 07-Analyst-Notes-and-SOC-Workflow/
│   ├── 01-Investigation-Checklist.md
│   └── 02-Day-37-Reflection.md
│
└── Screenshots/
    ├── 01-siem-log-sources.png
    ├── 02-splunk-linux-authentication.png
    ├── 03-splunk-sudo-investigation.png
    └── 04-asrep-roasting-lab.png
```

---

## 03 - SIEM Fundamentals

A SIEM provides a central location where security-relevant events can be collected and analysed.

The learning material describes logs arriving from many different resources.

Examples include workstations, servers, network devices, identity providers, cloud services, and applications.

The value is not simply storing logs.

The important capability is allowing an analyst to search and correlate events.

Correlation can connect activity from different systems.

This gives the analyst more context than a single isolated event.

A suspicious authentication event may become more meaningful when combined with host activity or network telemetry.

---

## 04 - Log Source Categories

### Host-Based

Host-based logs originate from individual devices.

Examples include workstations and servers.

Important areas include:

- Authentication
- Account Management
- System Events
- Process Auditing
- Object Access
- Policy Changes

These sources can support detection of suspicious account activity, privilege escalation, process execution, and unauthorised access.

### Network-Based

Network sources provide visibility into communication.

Examples include:

- Firewall logs
- IDS/IPS logs
- Router logs
- VPN logs
- DNS logs
- Proxy server logs

These can support investigation of scanning, suspicious external connections, repeated login attempts, and unusual traffic.

### Web-Based

Web infrastructure can generate:

- Web server logs
- WAF logs
- API gateway logs
- Web application logs
- CDN logs
- Load balancer logs

These can support investigation of SQL injection attempts, web-shell exploitation, and suspicious web requests.

---

## 05 - Time Pitfalls

Security investigations depend heavily on timestamps.

Different sources may use different time zones.

Some sources may use UTC.

Others may use local time.

Some logs may not contain timezone information.

A SIEM can also display data using a configured timezone.

Therefore, analysts must understand the timezone associated with each event.

A difference in displayed time does not automatically mean the events happened at different real-world times.

Timeline construction should account for timezone differences.

---

## 06 - Log Normalisation

Different systems do not necessarily format their logs in the same way.

The learning material gives JSON, XML, and plain text as examples.

Field names and structures can also differ.

Normalisation converts these different representations into a consistent structure.

This makes searching easier.

It also makes filtering and correlation easier.

Without normalisation, each source may require different field names and parsing logic.

---

## 07 - Splunk Practical Work

The practical work used Splunk to inspect events from task-specific indexes.

The investigations included Linux authentication activity and sudo activity.

The work also included Windows process and network-event searches.

The investigation approach was:

1. Identify the relevant index.
2. Start with a focused query.
3. Inspect returned events.
4. Identify useful fields.
5. Narrow the search.
6. Compare related events.
7. Establish a timeline.
8. Record the evidence.
9. Avoid assuming a conclusion without supporting events.

---

## 08 - Linux Investigation Notes

The Linux investigation used `auth.log` and the `linux_secure` sourcetype.

Authentication events provided information about login attempts.

Sudo events provided information about privileged activity.

The investigation included successful and unsuccessful authentication activity.

A useful analyst habit is to compare failed authentication with a later successful authentication.

This can help determine whether repeated failures were followed by a successful login.

The source IP should be recorded when it is available.

---

## 09 - Windows Investigation Notes

Windows security telemetry can provide information about process execution and network activity.

The practical searches used EventCode values and fields such as:

- `_time`
- `ComputerName`
- `User`
- `Image`
- `CommandLine`
- `Hashes`
- `SourceIp`
- `SourcePort`
- `DestinationIp`
- `DestinationPort`

These fields can help connect a process with its user and network behaviour.

---

## 10 - Active Directory Investigation

A separate Active Directory investigation was started on Hack The Box.

The target used during the exercise was:

`10.129.185.214`

The lab directs the analyst to inspect an evidence file named:

`Desktop/Evidence/Security-DC`

The investigation focuses on Kerberos Event ID `4768`.

The lesson identifies:

`Pre-Authentication Type = 0`

and:

`Ticket Encryption Type = 0x17`

These values are used as indicators for the exercise.

The account name and exact timestamp must be read from the relevant event.

Event ID `4768` itself is not the username.

---

## 11 - Current Status

| Area | Status |
|---|---|
| SIEM fundamentals | Completed |
| Host log sources | Completed |
| Network log sources | Completed |
| Web log sources | Completed |
| Time pitfalls | Completed |
| Log normalisation | Completed |
| Splunk practical work | Completed |
| Linux authentication | Completed |
| Sudo investigation | Completed |
| Active Directory AS-REP lab | In Progress |

---

## 12 - Evidence Standards

Evidence should be reproducible.

Record the query used.

Record the relevant timestamp.

Record the source.

Record the user, host, IP, process, or event identifier when applicable.

Capture screenshots when the lab requires visual evidence.

Do not publish credentials or secrets.

Do not mark an investigation as completed until the requested evidence has actually been verified.

---

## 13 - Day 37 Key Takeaways

A SIEM is valuable because it brings multiple telemetry sources together.

Different log sources answer different investigation questions.

Host logs show what happened on systems.

Network logs show how systems communicated.

Web logs show application-facing activity.

Authentication logs show identity-related activity.

Normalisation makes these datasets easier to search consistently.

Time synchronisation is critical for accurate timelines.

Splunk searches should progress from broad discovery to focused evidence.

The strongest investigations correlate multiple events instead of relying on one log entry.

---

## 14 - Next Step

The remaining Active Directory exercise will be continued manually.

The goal is to extract the requested evidence from the supplied Security-DC evidence rather than relying on an assumed answer.

Once complete, the final timestamp, account, and supporting evidence should be added to the investigation notes.
