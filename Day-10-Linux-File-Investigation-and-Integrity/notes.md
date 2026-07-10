# Practical Notes

## File Metadata Analysis

### Observation

- Inspected file ownership, permissions, timestamps, and metadata using `stat`.

### Key Learning

- Metadata provides valuable context during investigations.

### SOC Relevance

Modification time, ownership, and permissions help determine whether file activity is expected or suspicious.

---

## File Type Identification

### Observation

- Verified the actual file type using the `file` command.

### Key Learning

- File extensions can be misleading.

### SOC Relevance

Always verify the real file type before making conclusions.

---

## File Integrity

### Observation

- Generated SHA-256 hashes before and after modifying a file.

### Key Learning

- Even a small file modification produces a completely different hash.

### SOC Relevance

Hashes help verify file integrity and compare files against threat intelligence.

---

## File Discovery

### Observation

- Located files using the `find` command.

### Key Learning

- `find` performs real-time searches based on file attributes.

### SOC Relevance

Useful for locating recently modified or suspicious files during investigations.

---

## Executable Verification

### Observation

- Compared `which` and `whereis`.

### Key Learning

- `which` identifies the executable path.
- `whereis` identifies related program files.

### SOC Relevance

Unexpected executable locations should be investigated before drawing conclusions.
