# SOC Analyst Lessons

## 1. Correlate Artifacts
No single log line tells the entire story. Authentication and session artifacts answer different questions.

## 2. Prioritize Privileged Compromise
A successful SSH login to `root` should immediately increase incident priority.

## 3. Watch for Simple Persistence
A newly created local account placed into a privileged group can be an effective persistence mechanism.

## 4. Investigate Sudo Commands
Sudo logs can reveal exactly what an attacker executed with elevated privileges.

## 5. Build a Timeline
The strongest narrative is:

`Brute Force -> Compromise -> Interactive Access -> Persistence -> Privileged Execution`

## Example Correlation Logic
```text
IF repeated SSH failures from one source
AND successful authentication follows
AND target is privileged
THEN raise investigation priority

IF suspicious session
AND new local account
AND privileged-group membership change
THEN raise persistence alert

IF new account
AND sudo execution
AND external download
THEN escalate for post-exploitation investigation
```

## Final Assessment
Brutus demonstrates a compact incident-response workflow: identify the attacker, validate compromise, reconstruct the session, detect persistence, map the behavior and recover the final privileged action.
