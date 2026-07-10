# Linux File Investigation Interview Questions

## File Metadata

1. What information does the `stat` command provide?

2. Why is file metadata important during an investigation?

---

## File Identification

3. Why is the `file` command more reliable than checking a file extension?

4. What would you do if a `.pdf` file is identified as an executable?

---

## File Integrity

5. What is a cryptographic hash?

6. Why is SHA-256 preferred over MD5?

7. Can a SHA-256 hash alone prove a file is malicious?

---

## File Search

8. Explain the difference between `find` and `locate`.

9. How would you locate files modified within the last 24 hours?

---

## Executable Investigation

10. Explain the difference between `which` and `whereis`.

11. What would you investigate if `which python3` returned `/tmp/python3`?

---

## SOC Scenario

12. A suspicious executable is found in `/tmp`. Describe your investigation workflow.

13. What evidence would you collect before escalating an incident?

14. Why is evidence correlation important in SOC investigations?
