# Module 05 | Sysmon: Files & Network

## Relevant events
| Event ID | Purpose |
|---|---|
| 3 | Network connection |
| 11 | File creation |
| 13 | Registry value set |
| 22 | DNS query |

Use Process ID to connect these events back to Sysmon Event ID 1.

## Persistence evidence
Event ID 11 showed `ckjg.exe` creating:

`C:\Users\sarah.miller\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\DeleteApp.url`

User:
`THM-PC\sarah.miller`

## Network evidence
Event ID 3 showed:
- Source IP: `10.10.57.125`
- Destination IP: `193.46.217.4`
- Destination Port: `7777`
- Protocol: TCP

C2 endpoint:
`193.46.217.4:7777`

## DNS caution
An inspected Event ID 22 showed `wpad` with no result. That was not accepted as the malicious DNS evidence.

The correct method is to find the DNS event associated with the malware process and correlate its query/result with the C2 activity.

## Chain
ckjg.exe -> Event 11 persistence -> Event 3 C2 -> Event 22 DNS

## Lesson
Do not label the first DNS query as malicious. Correlate process, Process ID, query and result.
