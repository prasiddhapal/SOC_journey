# 👤 chown - Change File Ownership

## 🎯 Objective

Learn how to change file ownership and group ownership using the `chown` command.

---

## 💻 Commands

```bash
sudo chown famous soclabt.txt
sudo chown famous:famous soclabt.txt
ls -l soclabt.txt
```

---

## 🔍 Evidence

### Before

```text
-rw------- 1 window window 0 Jul 4 11:23 soclabt.txt
```

### After Changing Owner

```text
-rw------- 1 famous window 0 Jul 4 11:23 soclabt.txt
```

### After Changing Owner & Group

```text
-rw------- 1 famous famous 0 Jul 4 11:23 soclabt.txt
```

---

## 📊 Findings

| Attribute | Before | After |
|-----------|--------|-------|
| Owner | window | famous |
| Group | window | famous |
| Permissions | rw------- | rw------- (No Change) |

---

## 🛡️ Security Relevance

- `chown` changes file ownership without modifying permissions.
- Unexpected ownership changes on sensitive files may indicate privilege misuse or unauthorized administrative activity.
- During investigations, SOC analysts verify ownership changes to determine whether they were authorized.

---

## 🎤 Interview Questions

**Q1. What is the difference between `chmod` and `chown`?**

- `chmod` changes permissions.
- `chown` changes ownership.

**Q2. Does `chown` modify file permissions?**

No. It changes only the owner and/or group.

**Q3. Why is file ownership important?**

Ownership determines which user controls a file and is an important indicator during security investigations.

---

## 📚 Key Takeaway

File ownership and file permissions are different concepts. A SOC Analyst should always verify ownership when investigating unauthorized file modifications.

---

✅ **Status:** Completed

**Author:** Prasiddha Pal
