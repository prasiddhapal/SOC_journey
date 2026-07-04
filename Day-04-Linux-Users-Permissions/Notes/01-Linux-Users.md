# Linux Users

## 🎯 Objective

Understand how Linux identifies users and why user identity is important in system administration and SOC investigations.

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
| `whoami` | Display the currently logged-in user |
| `id` | Display user identity (UID, GID, and group membership) |
| `id famous` | Verify information about the newly created user |

---

## 🔍 Evidence

### Check Current User

```bash
whoami
```

**Output**

```text
window
```

---

### Display User Identity

```bash
id
```

**Output**

```text
uid=1000(window) gid=1000(window) groups=1000(window),4(adm),27(sudo),100(users),...
```

---

### Verify New User

```bash
id famous
```

**Output**

```text
uid=1001(famous) gid=1001(famous) groups=1001(famous),100(users)
```

---

## 🧠 Analysis

- `whoami` displays only the username of the currently logged-in user.
- `id` provides detailed identity information including UID, GID, and group memberships.
- Every Linux user is assigned a unique **User Identifier (UID)**.
- Group membership determines the privileges available to the user.
- User identity is the foundation of Linux authentication and authorization.

---

## 🛡️ Security Relevance

Understanding user identity is essential during security investigations.

A SOC Analyst uses user information to:

- Verify the account involved in an incident.
- Identify user privileges.
- Investigate unauthorized access attempts.
- Validate ownership during forensic investigations.

---

## 🎤 Interview Questions

### 1. What is the difference between `whoami` and `id`?

**Answer**

- `whoami` displays only the current username.
- `id` displays the username, UID, GID, and group memberships.

---

### 2. What is UID?

**Answer**

UID (User Identifier) is a unique numeric value assigned to every Linux user account.

---

### 3. Why is the `id` command useful for a SOC Analyst?

**Answer**

It helps identify the user's UID, GID, and group memberships, allowing analysts to understand the privileges associated with an account during an investigation.

---

## 📚 Key Takeaway

Linux identifies every user using a unique UID. While `whoami` provides the current username, the `id` command offers detailed identity information that is valuable during security investigations and access-control analysis.

---

## ✅ Status

**Completed**

---

## 👨‍💻 Author

**Prasiddha Pal**

SOC Analyst Learning Journey | Linux Security | Blue Team

**Day 04 – Linux Users**
