# Module 01 | Windows Logging Foundations

Windows events record operating-system activity and commonly expose Event ID, time, user, source and event details.

## Event Viewer workflow
1. Open Event Viewer.
2. Select the relevant log.
3. Filter by Event ID.
4. Review timestamps.
5. Open the event.
6. Inspect General and Details/XML views.
7. Record identifiers for correlation.

Windows EVTX files are stored under:
`C:\Windows\System32\winevt\Logs`

## Investigation questions
- Who performed the action?
- When did it happen?
- From where?
- What happened next?
- Which process performed it?
- What files changed?
- What network destination was contacted?

## Core identifiers
| Identifier | Purpose |
|---|---|
| Event ID | Activity type |
| Logon ID | Authentication/session correlation |
| Process ID | Sysmon correlation |
| Parent Process ID | Process ancestry |
| Source IP | Remote origin |
| Destination IP/Port | Network destination |

## Lesson
The useful SOC skill is correlating events into an attack timeline rather than memorising isolated Event IDs.
