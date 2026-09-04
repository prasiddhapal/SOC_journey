# Day 40 - Windows Memory Forensics

## Objective

Use Volatility 3 to extract kernel and process-level evidence from the memory image.

## Evidence File

```text
memdump.mem
```

## Q6 - Kernel Base

Command:

```bash
vol -f memdump.mem windows.info
```

The output showed:

```text
Kernel Base    0xf80079213000
```

### Q6 Answer

```text
0xf80079213000
```

## Q7 - Persistent Executable Path

Service/process investigation was performed with:

```bash
vol -f memdump.mem windows.svcscan
```

The process tree was then examined:

```bash
vol -f memdump.mem windows.pstree | grep -i -A 3 -B 3 updatenow
```

The suspicious process appeared as:

```text
w3wp.exe
└── updatenow.exe
```

The command line confirmed the full on-disk path:

```text
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup\updatenow.exe
```

### Q7 Answer

```text
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup\updatenow.exe
```

## Q8 - Process and PID

The process tree showed:

```text
4332  w3wp.exe
└── 900  updatenow.exe
```

`w3wp.exe` is the IIS worker process in this lab context.

### Q8 Answer

```text
w3wp.exe, PID 4332
```

## Persistence Significance

The executable resided in the Windows Startup directory:

```text
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup\
```

This is a strong persistence indicator because execution can occur through the Startup mechanism.

## Key Lesson

Memory forensics can reveal relationships that isolated file or network evidence cannot, especially parent-child process relationships, command lines, and persistence locations.
