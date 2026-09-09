# 05 - Process Correlation

## Notepad Observation
On `THM-MKT-WS`, process telemetry showed:

- Process: `Notepad.exe`
- PID: `9048`
- Time observed: approximately `21:19:53`

The process was present shortly before the `21:20:14` SMB write.

## Correlation Result
A time relationship exists:

`Notepad.exe PID 9048 -> shortly before -> SMB WriteData`

However, the available process telemetry did not provide a direct file-write event tying PID `9048` to `nathan brooks notes.txt`.

## Analyst Conclusion
**Notepad is a plausible process candidate, not a confirmed originating process.**

This distinction is retained in the final assessment.
