# Practical Notes

## Linux Capabilities

Linux Capabilities divide root privileges into smaller, specific privileges instead of granting full administrative access.

---

## Principle of Least Privilege

Applications should receive only the permissions required to perform their intended tasks.

---

## getcap

Displays Linux capabilities assigned to files.

Example:

```bash
getcap -r / 2>/dev/null
```

---

## setcap

Assigns or removes Linux capabilities from files.

Examples:

```bash
sudo setcap cap_net_bind_service=ep filename
```

```bash
sudo setcap -r filename
```

---

## SUID vs Capabilities

SUID grants the program the file owner's privileges.

Linux Capabilities grant only the required privilege, reducing the attack surface.

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
