# Linux Commands Reference – Day 17

---

# journalctl

## Purpose

View logs collected by systemd.

## Syntax

```bash
journalctl
journalctl -b
journalctl -u ssh
journalctl --since "today"
```

## SOC Use

- Authentication investigation
- Service troubleshooting
- Timeline analysis

---

# awk

## Purpose

Extract and process text fields.

## Syntax

```bash
awk '{print $1}'
awk '/Failed/'
```

## SOC Use

- Parse log files
- Extract usernames
- Count records

---

# sed

## Purpose

Edit text streams.

## Syntax

```bash
sed 's/Failed/ALERT/g'
sed -n '5,10p'
```

## SOC Use

- Redact reports
- Replace indicators
- Clean log output

---

# tr

## Purpose

Translate, delete, or squeeze characters.

## Syntax

```bash
tr 'A-Z' 'a-z'
tr -d '0-9'
tr -s ' '
```

## SOC Use

- Normalize log data
- Remove unwanted characters
- Format investigation output

---

# tee

## Purpose

Display command output while simultaneously writing it to a file.

## Syntax

```bash
command | tee report.txt
command | tee -a report.txt
```

## SOC Use

- Preserve investigation evidence
- Build forensic reports
- Maintain command output history

---

# xargs

## Purpose

Convert standard input into command-line arguments.

## Syntax

```bash
find . -name "*.log" | xargs grep "Failed"
```

## SOC Use

- Bulk file processing
- Multi-file searching
- Large-scale investigations
