# Practical Notes

## getpcaps

Displays Linux capabilities assigned to a running process.

Example:

```bash
getpcaps PID
```

---

## getcap vs getpcaps

- getcap → File capabilities
- getpcaps → Running process capabilities

---

## Capability Abuse

Attackers may assign dangerous capabilities such as `CAP_SYS_ADMIN` to binaries instead of using SUID to bypass simple detection methods.

---

## SOC Investigation Workflow

Verify

↓

Collect Evidence

↓

Analyze

↓

Correlate

↓

Document

↓

Escalate

---

## Evidence Collection

- Process
- Parent Process
- File Metadata
- SHA-256 Hash
- Network Connections
- User Information
- Authentication Logs
