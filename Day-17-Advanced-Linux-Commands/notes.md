# Day 17 Notes

## journalctl

- Displays systemd logs.
- Useful for investigating services and authentication events.

---

## awk

- Splits text into fields.
- Excellent for parsing log files.

---

## sed

- Stream editor.
- Modifies output without changing the original file unless `-i` is used.

---

## tr

- Translates or deletes characters.
- Useful for formatting investigation output.

---

## tee

- Displays output and writes it to a file simultaneously.
- `tee -a` appends instead of overwriting.

---

## xargs

- Reads input from stdin.
- Converts input into arguments for another command.
- Commonly used with `find`.
