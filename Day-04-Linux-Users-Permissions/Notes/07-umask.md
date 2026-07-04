# 🛡️ umask - Default File Permissions

## 🎯 Objective

Understand how the `umask` command controls the default permissions of newly created files and directories.

---

## 💻 Commands

```bash
umask
touch umask_test1.txt
ls -l umask_test1.txt

umask 077
touch umask_test2.txt
ls -l umask_test2.txt
```

---

## 🔍 Evidence

### Default umask

```text
0002
```

### Before Changing umask

```text
-rw-rw-r-- 1 window window 0 Jul 4 21:34 umask_test1.txt
```

### After `umask 077`

```text
-rw------- 1 window window 0 Jul 4 21:35 umask_test2.txt
```

---

## 📊 Findings

| Setting | New File Permission |
|---------|---------------------|
| `0002` | `rw-rw-r--` (664) |
| `077` | `rw-------` (600) |

---

## 🛡️ Security Relevance

- `umask` defines the default permissions assigned to newly created files.
- A restrictive `umask` reduces the risk of unauthorized access.
- SOC analysts review `umask` settings when investigating insecure default file permissions.

---

## 🎤 Interview Questions

**Q1. What is the purpose of `umask`?**

It defines the default permissions for newly created files and directories by removing unnecessary permissions.

**Q2. Does changing `umask` modify existing files?**

No. It only affects files and directories created after the new `umask` value is applied.

**Q3. Why is `umask 077` considered more secure than `umask 002`?**

Because it removes all permissions for the group and others, allowing only the owner to access newly created files.

---

## 📚 Key Takeaway

`umask` improves Linux security by automatically applying safer default permissions to new files and directories.

---

✅ **Status:** Completed

**Author:** Prasiddha Pal
