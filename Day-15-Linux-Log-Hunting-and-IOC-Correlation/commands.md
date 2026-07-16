# Commands Practiced

## Authentication Logs

```bash
cat /var/log/auth.log
```

```bash
journalctl
```

```bash
journalctl -n 20
```

```bash
journalctl -f
```

---

## GREP

```bash
grep "CRON" /var/log/auth.log
```

```bash
grep -i "failed" /var/log/auth.log
```

```bash
grep -n "CRON" /var/log/auth.log
```

```bash
grep -c "CRON" /var/log/auth.log
```

```bash
grep -v "CRON" /var/log/auth.log
```

```bash
grep -E "CRON|gdm-password" /var/log/auth.log
```
