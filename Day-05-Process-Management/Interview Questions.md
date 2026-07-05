# Interview Questions

## Q1. What is a Process?

A process is a program that is currently running.

---

## Q2. What is PID?

PID is a unique identifier assigned to every running process.

---

## Q3. What is PPID?

PPID identifies the parent process that started the current process.

---

## Q4. Difference between ps and top?

- ps provides a snapshot of running processes.
- top provides a real-time view of running processes and system resource usage.

---

## Q5. Difference between kill and kill -9?

- kill sends SIGTERM (15) for graceful termination.
- kill -9 sends SIGKILL (9) for immediate termination.

---

## Q6. Why is PPID important for SOC analysts?

PPID helps trace the origin of a process and understand parent-child relationships during investigations.

---

## Q7. Why shouldn't you immediately kill a high CPU process?

High CPU usage alone does not prove malicious activity. Always collect evidence before taking action.
