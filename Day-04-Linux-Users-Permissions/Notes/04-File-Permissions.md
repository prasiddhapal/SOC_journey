# 🔐 File Permissions in Linux

## 🎯 Objective

Understand Linux file permissions and analyze who can read, write, or execute a file.

---

## 💻 Commands

```bash
ls -l
```

---

## 🔍 Evidence

### Output

```text
-rw-rw-r-- 1 window window 0 Jul 4 11:23 soclabt.txt
```

### Permission Breakdown

```text
-rw-rw-r--
 │  │  │
 │  │  └── Others (r--)
 │  └───── Group (rw-)
 └──────── Owner (rw-)
```

---

## 📊 Findings

| User Type | Permission | Access |
|------------|------------|--------|
| Owner | `rw-` | Read, Write |
| Group | `rw-` | Read, Write |
| Others | `r--` | Read Only |

### Numeric Representation

| Symbolic | Numeric |
|-----------|---------|
| `rw-` | 6 |
| `r--` | 4 |

**Overall Permission:** `664`

---

## 🛡️ Security Relevance

- File permissions control access to system resources.
- Excessive permissions can expose sensitive information.
- SOC analysts review permissions to identify unauthorized access and security misconfigurations.

---

## 🎤 Interview Questions

**Q1. What does `-rw-rw-r--` mean?**

The owner and group have read/write permissions, while others have read-only access.

**Q2. What does the first `-` represent?**

It indicates that the object is a regular file.

**Q3. Is `664` secure?**

It depends on the business requirement. It is acceptable for shared files but not for confidential information.

---

## 📚 Key Takeaway

Linux file permissions determine who can access a file. Understanding both symbolic (`rw-r--r--`) and numeric (`644`, `664`, `755`) permissions is essential for Linux administration and SOC investigations.

---

✅ **Status:** Completed

**Author:** Prasiddha Pal
