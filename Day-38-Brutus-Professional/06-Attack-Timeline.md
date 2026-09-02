# Attack Timeline

| UTC Time | Event | Source |
|---|---|---|
| 2024-03-06 06:31:xx | SSH brute-force activity from `65.2.161.68` | auth.log |
| 2024-03-06 06:31:40 | Successful authentication to `root` | auth.log |
| 2024-03-06 06:32:44 | Successful root authentication | auth.log |
| 2024-03-06 06:32:45 | Interactive root session begins | wtmp |
| 2024-03-06 06:34:18 | `cyberjunkie` account/group creation | auth.log |
| 2024-03-06 06:35:15 | `cyberjunkie` added to sudo | auth.log |
| 2024-03-06 06:37:24 | First attacker root session closes | auth.log |
| 2024-03-06 06:39:38 | Privileged curl command executed | auth.log |

## Attack Chain
```text
SSH Brute Force
      |
      v
Successful Root Authentication
      |
      v
Interactive Root Session
      |
      v
Create cyberjunkie
      |
      v
Add cyberjunkie to sudo
      |
      v
Sudo as Root
      |
      v
Download External Script
```
