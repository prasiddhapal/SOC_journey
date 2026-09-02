# MITRE ATT&CK Mapping

## T1136.001 - Create Account: Local Account

The attacker created the local account `cyberjunkie` and granted it membership in the `sudo` group.

This behavior maps to **Create Account: Local Account**, a persistence sub-technique.

## Supporting Behaviors
The investigation also exposed:
- SSH brute-force activity
- successful privileged-account authentication
- local account creation
- privileged-group modification
- sudo execution
- external script retrieval

Only T1136.001 is recorded here as the explicit persistence mapping from the investigation.
