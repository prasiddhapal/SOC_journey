# Practical Notes

## SUID

- Executes a program with the file owner's permissions.
- Common examples include `passwd`, `sudo`, and `su`.

### SOC Relevance

Investigate unexpected SUID files before taking action.

---

## SGID

- Executes a program with the file group's permissions.
- On directories, new files inherit the directory's group.

### SOC Relevance

Verify whether SGID is expected for shared applications or directories.

---

## Sticky Bit

- Used mainly on shared directories.
- Prevents users from deleting files owned by other users.

### Example

```text
drwxrwxrwt
```

---

## Ownership Investigation

Useful commands:

- id
- groups
- ls -l
- stat

Ownership helps identify which user or group created or modified a file.

---

## chgrp

Changes only the group ownership of a file.

Example:

```bash
chgrp docker demo.txt
```

### Observation

Owner remains unchanged while the group changes.

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
