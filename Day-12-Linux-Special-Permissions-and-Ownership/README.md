# Linux Special Permissions and Ownership for SOC Analysts

## 📖 Introduction

Linux special permissions provide controlled privilege escalation and secure file sharing. Understanding SUID, SGID, Sticky Bit, and file ownership is essential for SOC analysts investigating privilege abuse, unauthorized access, and suspicious system changes.

---

## 🎯 Learning Objectives

- Understand SUID, SGID, and Sticky Bit.
- Identify files with special permissions.
- Investigate file ownership and group ownership.
- Understand the purpose of `id`, `groups`, and `chgrp`.
- Apply a security-first investigation workflow.

---

## 📚 Topics Covered

### Linux Special Permissions

- SUID
- SGID
- Sticky Bit

### Ownership Investigation

- File Owner
- Group Ownership
- User Identity
- Group Membership

### Commands

- find
- id
- groups
- ls -l
- stat
- chgrp

### SOC Investigation

- Suspicious SUID binaries
- Ownership analysis
- Group permission investigation
- Evidence collection
- Incident escalation

---

## 🛡️ Practical Activities

- Identified SUID files
- Identified SGID files
- Identified Sticky Bit directories
- Investigated user and group information
- Practiced changing file group ownership using `chgrp`

---

## 📂 Documentation

- Commands → commands.md
- Notes → notes.md
- Interview Questions → interview_questions.md

---

## 📸 Screenshots

- SUID Analysis
- SGID Analysis
- Sticky Bit Analysis
- Ownership Investigation
- CHGRP Demonstration

---

## 🎯 Key Takeaways

- SUID executes programs with the file owner's privileges.
- SGID executes programs with the file group's privileges and enables group inheritance on directories.
- Sticky Bit protects files in shared directories from unauthorized deletion.
- Ownership and group information are critical pieces of evidence during investigations.
- SOC analysts investigate before making changes.
