# 04 — Runtime Monitoring

## Objective

Understand why runtime monitoring is necessary for questions such as:

- Which programs were launched?
- Which files were accessed?
- What network connections were made?
- What process performed an action?

## System calls

The training introduced system calls as the interface between applications and the Linux kernel.

The `execve` system call is commonly used when a program is executed.

## Why runtime visibility matters

Authentication logs can tell us that a user logged in, but they do not necessarily tell us everything the user did afterward.

Runtime monitoring can connect:

```text
User
  ↓
Process
  ↓
Command
  ↓
File / Network activity
```

This creates a more useful investigation timeline.

## SOC lesson

The broader the telemetry, the more activity can be investigated, but excessive logging can also create large volumes of data. Effective monitoring focuses on useful, high-risk events.
