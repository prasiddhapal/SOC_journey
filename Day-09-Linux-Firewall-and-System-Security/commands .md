# Commands Practiced

## Firewall Status

```bash
sudo ufw status
```

```bash
sudo ufw status verbose
```

```bash
sudo ufw status numbered
```

---

## Firewall Rules

```bash
sudo ufw allow ssh
```

```bash
sudo ufw allow 22/tcp
```

```bash
sudo ufw deny 23/tcp
```

```bash
sudo ufw delete allow 23/tcp
```

---

## Firewall Management

```bash
sudo ufw reload
```

```bash
sudo ufw reset
```

---

## Application Profiles

```bash
sudo ufw app list
```

```bash
sudo ufw app info OpenSSH
```
