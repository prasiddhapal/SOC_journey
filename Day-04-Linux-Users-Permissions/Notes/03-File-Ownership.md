# 📂 File Ownership in Linux

## 🎯 Objective

Understand Linux file ownership and investigate how ownership changes using the `chown` command.

---

## 💻 Commands

```bash
touch soclabt.txt
ls -l soclabt.txt
sudo chown famous soclabt.txt
sudo chown famous:famous soclabt.txt
```

---

## 🔍 Evidence

### Before

```text
-rw------- 1 window window 0 Jul 4 11:23 soclabt.txt
```

### After `chown famous`

```text
-rw------- 1 famous window 0 Jul 4 11:23 soclabt.txt
```

### After `chown famous:famous`

```text
-rw------- 1 famous famous 0 Jul 4 11:23 soclabt.txt
```

---

## 📊 Findings

| Item | Before | After |
|------|--------|-------|
| Owner | window | famous |
| Group | window | famous |
| Permissions | rw------- | rw------- |

---

## 🛡️ Security Relevance

- File ownership determines which user controls a file.
- Unexpected ownership changes may indicate privilege escalation or unauthorized administrative activity.
- SOC analysts verify ownership when investigating suspicious system modifications.

---

## 🎤 Interview Questions

**Q1. What is the difference between `chmod` and `chown`?**

- `chmod` changes file permissions.
- `chown` changes file ownership.

**Q2. Does `chown` modify file permissions?**

No. It changes only the owner and/or group.

---

## 📚 Key Takeaway

`chown` changes file ownership without affecting file permissions. Monitoring ownership changes helps identify unauthorized modifications during security investigations.

---

✅ **Status:** Completed

**Author:** Prasiddha Pal
