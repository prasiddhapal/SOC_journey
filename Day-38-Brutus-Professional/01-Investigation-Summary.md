# Investigation Summary

## Scenario
A Linux/Confluence server was subjected to SSH brute-force activity. After successful access, the attacker performed post-compromise actions including persistence and privileged command execution.

## Primary Questions
- Which IP conducted the brute force?
- Which account was compromised?
- When did the interactive session begin?
- Which SSH session number was used?
- Which account was created for persistence?
- Which ATT&CK sub-technique describes that persistence?
- When did the first attacker session end?
- What privileged command downloaded a script?

## Method
`auth.log` was used for authentication, PAM sessions, account/group changes and sudo commands. `wtmp` was used to reconstruct the interactive login session.

The key timeline distinction was between authentication time and actual terminal-session start time.

## Result
The evidence supports a coherent attack lifecycle: credential guessing, privileged compromise, interactive access, persistence establishment and privileged script retrieval.
