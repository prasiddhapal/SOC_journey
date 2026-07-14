# Commands Practiced

## Check getpcaps Installation

```bash
which getpcaps
```

## Find Running Process

```bash
ps -ef | grep ping
```

## Display Process Capabilities

```bash
getpcaps PID
```

## Display File Capabilities

```bash
getcap /usr/bin/ping
```

## Process Information

```bash
ps -fp PID
```

## Parent Process

```bash
pstree -p
```

## File Metadata

```bash
ls -l
stat
file
```

## File Hash

```bash
sha256sum filename
```

## Active Network Connections

```bash
ss -tunap
```

## User Information

```bash
id
groups
```

## Authentication Logs

```bash
journalctl
```

or

```bash
cat /var/log/auth.log
```
