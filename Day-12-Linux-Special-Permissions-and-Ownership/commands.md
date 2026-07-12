# Commands Practiced

## Find SUID Files

```bash
find / -perm -4000 2>/dev/null
```

## Find SGID Files

```bash
find / -perm -2000 2>/dev/null
```

## Find Sticky Bit Directories

```bash
find / -perm -1000 2>/dev/null
```

## Check Sticky Bit

```bash
ls -ld /tmp
```

## User Information

```bash
id
```

```bash
groups
```

## File Ownership

```bash
ls -l
```

```bash
stat filename
```

## Change Group Ownership

```bash
chgrp docker demo.txt
```
