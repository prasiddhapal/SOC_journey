# Day 31 - Investigation

## Scenario

A financial institution's SIEM flagged unusual activity on an internal workstation with access to sensitive financial data.

A memory dump was provided for forensic analysis.

## Evidence

```text
192-Reveal.dmp
```

The image was analyzed with Volatility 3.

## 1. Validate Memory Image

```bash
vol -f 192-Reveal.dmp windows.info
```

The image was successfully interpreted as a Windows memory image and the required symbol information was loaded.

## 2. Enumerate Processes

```bash
vol -f 192-Reveal.dmp windows.pslist
```

The investigation identified:

```text
powershell.exe
PID: 3692
```

## 3. Review Process Tree

```bash
vol -f 192-Reveal.dmp windows.pstree
```

The process relationship showed:

```text
PID: 3692
PPID: 4120
```

## 4. Review Command Line

```bash
vol -f 192-Reveal.dmp windows.cmdline --pid 3692
```

The command line exposed suspicious PowerShell execution and `rundll32.exe` activity.

The remote infrastructure was:

```text
45.9.74.32:8888
```

The second-stage payload was:

```text
3435.dll
```

## 5. Identify Remote Share

The command line referenced:

```text
davwwwroot
```

This connected the endpoint execution with the remote resource.

## 6. Attribute the Process

```bash
vol -f 192-Reveal.dmp windows.getsids --pid 3692
```

The malicious process was associated with:

```text
Elon
```

## 7. ATT&CK Mapping

The DLL execution through `rundll32.exe` maps to:

```text
T1218.011 - Rundll32
```

## 8. Malware Correlation

The completed challenge identified the malware family as:

```text
STRELASTEALER
```

## Investigation Conclusion

Multiple correlated artifacts indicate compromise:

```text
powershell.exe
+
PID/PPID relationship
+
suspicious command line
+
remote WebDAV resource
+
3435.dll
+
rundll32.exe
+
compromised account
```

The evidence supports treating the workstation as compromised and continuing containment and enterprise-wide hunting.
