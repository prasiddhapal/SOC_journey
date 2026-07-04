# Linux Groups

## 🎯 Objective

Understand the purpose of Linux groups, how they simplify permission management, and why group membership is important during security investigations.

---

## 🖥️ Lab Environment

| Field | Details |
|--------|---------|
| Operating System | Kali Linux |
| Shell | Bash |
| User | window |
| Analyst | Prasiddha Pal |

---

## 💻 Commands Executed

| Command | Purpose |
|----------|---------|
| `id` | Display the current user's UID, GID, and group memberships |
| `id famous` | Display group information for the newly created user |
| `groups` | Display the groups of the current user |
| `getent group famous` | Verify that the `famous` group exists |
| `getent group users` | Verify that the `users` group exists |

---

## 🔍 Evidence

### Display Current User Groups

```bash
id
```

**Sample Output**

```text
uid=1000(window)
gid=1000(window)
groups=1000(window),4(adm),27(sudo),100(users),139(docker),...
```

---

### Verify New User

```bash
id famous
```

**Sample Output**

```text
uid=1001(famous)
gid=1001(famous)
groups=1001(famous),100(users)
```

---

### Verify Groups

```bash
getent group famous
```

```text
famous:x:1001:
```

```bash
getent group users
```

```text
users:x:100:
```

---

## 🧠 Analysis

- A Linux group is a collection of users that share common permissions.
- Every user has a **primary group (GID)** and may belong to multiple secondary groups.
- Group membership simplifies permission management across multiple users.
- The `id` command displays all groups associated with a user.
- The `getent` command verifies whether a group exists in the system database.

---

## 🛡️ Security Relevance

Group membership directly affects user privileges.

During a security investigation, a SOC Analyst checks:

- Whether a compromised account belongs to privileged groups.
- Whether a user has unnecessary group memberships.
- Whether unauthorized group modifications have occurred.
- Whether access permissions follow the Principle of Least Privilege.

---

## 🎤 Interview Questions

### 1. What is the difference between UID and GID?

**Answer**

- **UID (User Identifier)** uniquely identifies a user.
- **GID (Group Identifier)** identifies the user's primary group.

---

### 2. Why are Linux groups used?

**Answer**

Linux groups simplify permission management by allowing multiple users to share the same access permissions.

---

### 3. What is the purpose of the `getent` command?

**Answer**

`getent` retrieves user or group information from the system's configured databases and helps verify whether a user or group exists.

---

## 📚 Key Takeaway

Linux groups provide an efficient way to manage permissions for multiple users. Understanding group membership is essential for investigating user privileges, access control, and potential security misconfigurations.

---

## ✅ Status

**Completed**

---

## 👨‍💻 Author

**Prasiddha Pal**

SOC Analyst Learning Journey | Linux Security | Blue Team

**Day 04 – Linux Groups**
