# Interview Questions

## Q1. Why would you use `less` instead of `cat`?

**Answer**

`less` allows efficient navigation through large files without displaying the entire file at once.

---

## Q2. How do you count failed SSH login attempts?

**Answer**

```bash
grep "Failed" /var/log/auth.log | wc -l
```

---

## Q3. What is the purpose of `tail -f`?

**Answer**

It monitors a log file in real time and displays new log entries as they are written.
