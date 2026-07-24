# Linux Logging Notes

## cat

Displays the entire contents of a file.

Best for:
- Small files
- Configuration files

Not recommended for very large log files.

---

## less

Displays a file page by page.

Useful for:
- Large log files
- Searching within files
- Efficient navigation

---

## grep

Searches for matching patterns in a file.

Example:

```bash
grep "Failed" /var/log/auth.log
```

Displays only failed authentication events.
