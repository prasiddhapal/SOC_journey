# Day 40 - SMB Enumeration & Web-Shell Deployment

## Objective

Determine which SMB shares were probed and identify the malicious web-accessible payload.

## Q3 - SMB Share Discovery

SMB2 Tree Connect requests were inspected:

```bash
tshark -r capture.pcapng -Y "smb2.cmd == 3" -T fields -e frame.time -e ip.src -e ip.dst -e smb2.cmd -e smb2.tree
```

The first two distinct shares observed were:

```text
\\10.0.2.15\IPC$
\\10.0.2.15\Documents
```

### Q3 Answer

```text
\\10.0.2.15\IPC$
\\10.0.2.15\Documents
```

## Q4 - Malicious File Upload

HTTP request URIs were examined:

```bash
tshark -r capture.pcapng -Y "http.request" -T fields -e frame.time -e ip.src -e ip.dst -e http.request.uri
```

The malicious request referenced:

```text
/Documents/shell.aspx
```

Traffic validation showed the upload/access path was associated with the IIS host on TCP/80.

### Q4 Answer

```text
shell.aspx
```

## Attack Progression

```text
SMB Enumeration
      ↓
Documents Share
      ↓
Web-accessible location
      ↓
shell.aspx
      ↓
Remote Code Execution
```

## Key Lesson

A file name alone is not enough to establish malicious activity. Correlate the URI, source/destination, protocol, timing, and surrounding traffic.
