# 🔒 chmod - Change File Permissions

## 🎯 Objective

Learn how to modify Linux file permissions using the `chmod` command and verify the changes.

---

## 💻 Commands

```bash
touch secret.txt
ls -l secret.txt
chmod 600 secret.txt
ls -l secret.txt
```

---

## 🔍 Evidence

### Before

```text
-rw-rw-r-- 1 window window 0 Jul 4 11:23 secret.txt
```

### Command

```bash
chmod 600 secret.txt
```

### After

```text
-rw------- 1 window window 0 Jul 4 11:23 secret.txt
```

---

## 📊 Findings

| Before | After |
|---------|-------|
| `rw-rw-r--` | `rw-------` |
| Owner & Group had access | Only Owner has access |

---

## 🛡️ Security Relevance

- `chmod` modifies file permissions without changing ownership.
- Restricting permissions protects sensitive files from unauthorized access.
- Applying the Principle of Least Privilege reduces security risks.

---

## 🎤 Interview Questions

**Q1. What is the purpose of `chmod`?**

It modifies the permissions of a file or directory.

**Q2. What does `chmod 600` mean?**

The owner has read and write permissions, while the group and others have no permissions.

**Q3. Does `chmod` change file ownership?**

No. It only changes file permissions.

---

## 📚 Key Takeaway

The `chmod` command is used to control file access. Restricting permissions with `chmod 600` ensures that only the file owner can read or modify the file.

---

✅ **Status:** Completed

**Author:** Prasiddha Pal
