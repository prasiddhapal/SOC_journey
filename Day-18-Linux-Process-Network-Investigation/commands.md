# Commands - Day 18

## Process Investigation

| Command | Description |
|---------|-------------|
| `ps` | Show current processes |
| `ps -e` | Show all running processes |
| `ps aux` | Detailed process information |
| `ps -fp <PID>` | Show full details of a process |
| `ps aux --sort=-%cpu \| head` | Top CPU processes |
| `ps aux --sort=-%mem \| head` | Top memory processes |

---

## Real-Time Monitoring

| Command | Description |
|---------|-------------|
| `top` | Live system monitoring |
| `top -p <PID>` | Monitor a specific process |

### Useful Keys

- `P` → Sort by CPU
- `M` → Sort by Memory
- `T` → Sort by Runtime
- `L` → Search process
- `k` → Kill process
- `q` → Quit

---

## Network Investigation

| Command | Description |
|---------|-------------|
| `ss` | Show sockets |
| `ss -t` | TCP connections |
| `ss -u` | UDP connections |
| `ss -l` | Listening ports |
| `ss -tulp` | Listening ports with process |
| `ss -tnp` | Active TCP connections with PID |

---

## Open Files

| Command | Description |
|---------|-------------|
| `lsof` | List open files |
| `lsof -i` | Network connections |
| `lsof -iTCP` | TCP connections |
| `lsof -iUDP` | UDP connections |
| `lsof -p <PID>` | Open files for a process |

---

## Process Management

| Command | Description |
|---------|-------------|
| `kill <PID>` | Gracefully stop a process |
| `kill -9 <PID>` | Force stop a process |
| `kill -l` | List available signals |

---

## Process Search

| Command | Description |
|---------|-------------|
| `pgrep <name>` | Find process PID |
| `pgrep -l <name>` | PID with process name |
| `pgrep -a <name>` | PID with full command |
| `pgrep -n <name>` | Newest process |
| `pgrep -o <name>` | Oldest process |
| `pkill <name>` | Kill process by name |
| `pkill -9 <name>` | Force kill by name |

---

## Key Takeaways

- Verify before killing a process.
- Use `ps` and `top` for process analysis.
- Use `ss` and `lsof` for network investigation.
- Prefer `SIGTERM` before `SIGKILL`.
- Collect evidence before containment.
