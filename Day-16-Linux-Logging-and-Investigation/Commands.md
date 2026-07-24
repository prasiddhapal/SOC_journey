# Linux Log Analysis Commands

## View Entire File

```bash
cat /var/log/auth.log
```

---

## Read Large File

```bash
less /var/log/auth.log
```

---

## First 20 Lines

```bash
head -20 /var/log/auth.log
```

---

## Last 20 Lines

```bash
tail -20 /var/log/auth.log
```

---

## Real-Time Monitoring

```bash
tail -f /var/log/auth.log
```

---

## Search Failed Logins

```bash
grep "Failed" /var/log/auth.log
```

---

## Count Failed Logins

```bash
grep "Failed" /var/log/auth.log | wc -l
```

---

## Extract Usernames

```bash
cut -d ":" -f1 /etc/passwd
```

---

## Sort Data

```bash
sort users.txt
```

---

## Count Duplicate Entries

```bash
sort users.txt | uniq -c
```
