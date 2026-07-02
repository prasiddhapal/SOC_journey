# 🛡️ Commands Reference

## 🎯 Objective

Maintain a quick reference of all commands used during the SSH authentication investigation.

---

| Command | Purpose |
|---------|---------|
| `sudo systemctl status ssh` | Verify SSH service status |
| `sudo systemctl start ssh` | Start SSH service |
| `ss -tlnp \| grep :22` | Verify SSH is listening on TCP port 22 |
| `ssh window@127.0.0.1` | Initiate an SSH connection to the local system |
| `grep sshd /var/log/auth.log` | Analyze SSH authentication log entries |

---

## 💡 Key Takeaways

- Verify the service before investigating logs.
- Generate authentication events before analysis.
- Review only relevant log entries using `grep`.
- Keep frequently used commands documented for quick reference.
