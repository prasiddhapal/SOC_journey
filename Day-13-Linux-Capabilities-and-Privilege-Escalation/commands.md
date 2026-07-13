# Commands Practiced

## Check getcap Installation

```bash
which getcap
```

---

## Enumerate Linux Capabilities

```bash
getcap -r / 2>/dev/null
```

---

## Assign a Capability

```bash
sudo setcap cap_net_bind_service=ep filename
```

---

## Verify Assigned Capability

```bash
getcap filename
```

---

## Remove Capability

```bash
sudo setcap -r filename
```
