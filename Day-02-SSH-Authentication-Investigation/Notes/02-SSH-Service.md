# 🛡️ SSH Service Verification

## 🎯 Objective

Verify that the SSH service is running and listening before investigating authentication events.

---

## 📖 Concept

The SSH service runs as the **sshd (Secure Shell Daemon)** process. Before analyzing SSH logs, a SOC analyst should verify that the service is active. If the service is stopped, no new SSH authentication events will be generated.

---

## 🧪 Commands

### Check SSH Service Status

```bash
sudo systemctl status ssh
```

### Start SSH Service

```bash
sudo systemctl start ssh
```

### Verify Port 22

```bash
ss -tlnp | grep :22
```

---

## 📸 Screenshots

### SSH Service Status

```
../screenshots/01-ssh-service-status.png
```

### SSH Listening on Port 22

```
../screenshots/02-ssh-listening-port22.png
```

---

## 🔍 Observation

- SSH service was initially inactive.
- After starting the service, it became active.
- SSH was listening on TCP Port **22**.
- The service accepted both IPv4 and IPv6 connections.

---

## 🛡️ SOC Analysis

Before analyzing authentication logs, verifying that the SSH service is running ensures the generated logs are valid and current. This is a standard first step in an SSH investigation.

---

## 💡 Key Takeaways

- SSH server process is **sshd**.
- Default SSH port is **22/TCP**.
- `systemctl` is used to manage services.
- `ss` verifies listening network ports.

---

## 🎤 Interview Question

**Q:** Why should a SOC analyst verify the SSH service before investigating logs?

**A:** Because an inactive SSH service cannot generate authentication events. Verifying the service confirms that the logs being analyzed are current and relevant.
