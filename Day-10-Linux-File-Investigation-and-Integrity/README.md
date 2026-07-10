# Linux File Investigation and Integrity for SOC Analysts

## 📖 Introduction

File investigation is a fundamental skill for Security Operations Center (SOC) analysts. During security incidents, analysts must verify file types, inspect metadata, validate file integrity, and locate suspicious files before making any security decisions.

This lab focuses on practical Linux commands used for file investigation and integrity verification in real-world SOC environments.

---

## 🎯 Learning Objectives

- Understand Linux file metadata
- Identify file types using the `file` command
- Verify file integrity with SHA-256 hashes
- Locate suspicious files using `find`
- Differentiate between `find`, `locate`, `which`, and `whereis`
- Apply an evidence-based investigation workflow

---

## 📚 Topics Covered

### File Investigation

- File Metadata
- File Type Identification
- File Integrity
- File Hashing

### Linux Commands

- stat
- file
- find
- sha256sum
- which
- whereis

### SOC Investigation

- File Verification
- Metadata Analysis
- Hash Verification
- Evidence Collection
- Investigation Workflow

---

## 🛡️ Practical Investigation

During this lab:

- Examined file metadata using `stat`
- Identified file types using `file`
- Located files using `find`
- Generated SHA-256 hashes to verify file integrity
- Compared executable paths using `which`
- Identified related program locations using `whereis`
- Applied an evidence-based investigation process

---

## 📂 Documentation

- Commands → commands.md
- Notes → notes.md
- Interview Questions → interview_questions.md

---

## 📸 Screenshots

- File Command Analysis
- File Metadata Analysis
- Find Command Analysis
- SHA-256 Analysis
- Which & Whereis Analysis

---

## 🎯 Key Takeaways

- File extensions should never be trusted without verification.
- SHA-256 provides reliable file integrity verification.
- File metadata helps establish investigation timelines.
- File investigation requires correlating multiple sources of evidence before taking action.
