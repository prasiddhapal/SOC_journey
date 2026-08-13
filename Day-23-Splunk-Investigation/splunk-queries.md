# Splunk Queries

## 1. View Events

```spl
index=main
| sort 0 _time
| table _time host user event_id logon_type src_ip process parent pid command action
```

Used to build the investigation timeline.

---

## 2. Event ID 4688 - Process Creation

```spl
index=main event_id=4688
| table _time user process parent pid command
```

Observed:

- `powershell.exe` → parent `explorer.exe`
- PID: `4216`
- Command: `powershell.exe -NoProfile`
- `cmd.exe` → parent `powershell.exe`
- PID: `4332`
- Command: `cmd.exe /c whoami`

---

## 3. Event ID 4624 - Successful Logon

```spl
index=main event_id=4624
| table _time host user logon_type src_ip action
```

Observed:

- User: `Administrator`
- Logon Type: `3`
- Source IP: `10.49.108.37`
- Action: `successful_logon`

---

## 4. Source IP Investigation

```spl
index=main src_ip=10.49.108.37
| table _time host user event_id logon_type src_ip action
```

Used to identify authentication activity from the source IP.

---

## 5. Correlate Events

```spl
index=main
| sort 0 _time
| table _time event_id user src_ip process parent pid command action
```

Timeline:

```text
4624 → Successful Logon
      ↓
Administrator
      ↓
10.49.108.37
      ↓
4688 → powershell.exe
      ↓
4688 → cmd.exe /c whoami
```

---

## 6. Event Count

```spl
| eventcount summarize=false index=*
```

Used to verify whether Splunk indexes contain events.

---

## 7. Filter by Source IP

```spl
index=main src_ip=10.49.108.37
| stats count by src_ip
```

---

## 8. Investigation Lesson

The main lesson was **correlation**.

Do not investigate an event in isolation.

Correlate:

```text
User
Source IP
Authentication
Process
Parent Process
PID
Command Line
Timeline
```

The observed activity is suspicious and requires further investigation, but
the available events alone are not enough to prove malicious activity.
