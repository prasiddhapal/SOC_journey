# Linux User Management

User account auditing is an important task for SOC analysts to identify unauthorized users, privilege escalation, and persistence mechanisms.

---

# View User Accounts

```bash
cat /etc/passwd
```

Displays all local user accounts.

Each entry contains:

- Username
- UID
- GID
- Home Directory
- Login Shell

---

# View Groups

```bash
cat /etc/group
```

Displays all system groups and their members.

Review privileged groups such as:

- sudo
- wheel
- docker
- adm

---

# Query User Information

```bash
getent passwd <username>
```

Retrieves user information from local files or directory services like LDAP/Active Directory.

Example:

```bash
getent passwd window
```

---

# Check User Identity

```bash
id
```

Displays:

- User ID (UID)
- Group ID (GID)
- Supplementary groups

Useful for verifying user privileges.

---

# List User Groups

```bash
groups
```

Shows all groups assigned to the current user.

---

# SOC Investigation Tips

During an investigation, look for:

- Unexpected UID 0 accounts
- Unknown or recently created users
- Interactive login shells (`/bin/bash`)
- Unauthorized sudo group membership
- Accounts with unusual home directories

---

# Common Indicators

🚩 Multiple privileged users

🚩 Unknown administrator accounts

🚩 Users added to the `sudo` or `docker` group

🚩 Backdoor accounts created after suspicious logins

User account auditing helps detect privilege escalation and attacker persistence on Linux systems.
