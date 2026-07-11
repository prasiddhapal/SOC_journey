# Practical Notes

## Archive vs Compression

### Key Learning

- Archives combine multiple files into a single package.
- Compression reduces file size.
- `.tar.gz` combines both archiving and compression.

---

## TAR

### Observation

- Created, listed, and extracted archives.

### SOC Relevance

Inspect archive contents before extraction whenever possible.

---

## GZIP

### Observation

- Compressed and decompressed files.

### Key Learning

- Small files may become larger because compression metadata adds overhead.
- Large files benefit significantly from compression.

### SOC Relevance

Compressed log files are common during investigations.

---

## ZIP

### Observation

- Created ZIP archives and viewed contents safely.

### Key Learning

- ZIP archives both package and compress files.
- `unzip -l` allows inspection without extraction.

### SOC Relevance

Never extract untrusted archives without verification and following organizational procedures.

---

## Investigation Workflow

Receive Archive
↓

Verify Source

↓

Inspect Contents

↓

Analyze Safely

↓

Extract (If Required)

↓

Investigate Files

↓

Document Findings

↓

Escalate (If Required)
