# Practical Labs – Day 17

## Lab 1 – journalctl

### Objective

Investigate system logs.

### Commands

```bash
journalctl
journalctl -b
journalctl -u ssh
```

---

## Lab 2 – awk

### Objective

Extract information from log files.

### Commands

```bash
awk '{print $1}'
awk '/Failed/'
```

---

## Lab 3 – sed

### Objective

Modify output streams.

### Commands

```bash
sed 's/Failed/ALERT/g'
```

---

## Lab 4 – tr

### Objective

Translate and delete characters.

### Commands

```bash
tr 'A-Z' 'a-z'
tr -d '0-9'
```

---

## Lab 5 – tee

### Objective

Preserve investigation evidence.

### Commands

```bash
date | tee report.txt
hostname | tee -a report.txt
uptime | tee -a report.txt
```

### Learning Outcome

Evidence can be displayed and saved simultaneously.

---

## Lab 6 – xargs

### Objective

Process multiple files.

### Commands

```bash
find . -name "*.log" | xargs ls -lh

find /var/log -name "*.log" | xargs grep "Failed"

ls *.log | xargs wc -l
```

### Learning Outcome

Efficiently process multiple files during investigations.
