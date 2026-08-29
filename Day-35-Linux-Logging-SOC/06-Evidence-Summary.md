# 06 — Evidence Summary

## Evidence 1 — Suspicious SSH activity

**Source:** `/var/log/auth.log`

A source IP repeatedly generated failed SSH authentication attempts against multiple usernames:

```text
10.14.94.82
```

**Why it matters:** This pattern is consistent with password guessing, account enumeration, or other unauthorized authentication attempts.

---

## Evidence 2 — Privileged account creation

**Source:** `/var/log/auth.log`

The logs recorded creation of:

```text
xerxes
```

and addition of the account to:

```text
sudo
```

**Why it matters:** A newly created privileged account can provide persistence or elevated access.

---

## Evidence 3 — Tool installation

**Source:** `/var/log/apt/history.log` and `/var/log/dpkg.log`

Installed package:

```text
unzip 6.0-28ubuntu4.1
```

**Why it matters:** Package-manager records can provide supporting evidence for the installation of investigation-relevant tooling.

---

## Evidence 4 — Sensitive file access

**Source:** `auditd`

The audit trail recorded:

```bash
cat /secret.thm
```

**Why it matters:** Access to a sensitive file is a useful indicator when reconstructing attacker objectives.

---

## Evidence 5 — Network scanning

**Source:** `auditd`

The `naabu` binary was executed against:

```text
192.168.50.0/24
```

with:

```bash
-top-ports 4
```

**Why it matters:** Network scanning can indicate reconnaissance following host access.

---

## Final assessment

The strongest evidence comes from correlation rather than any individual event:

**SSH activity → account changes → tooling/history → sensitive file access → network reconnaissance**

This demonstrates the core SOC principle of building an evidence-backed timeline.
