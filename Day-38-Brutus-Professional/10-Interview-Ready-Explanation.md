# Interview-Ready Explanation

## 60-Second Summary
I investigated a Linux server compromise using `auth.log` and `wtmp`. I identified repeated SSH failures from `65.2.161.68`, correlated them with successful access to `root`, and used `wtmp` to determine the actual interactive session timestamp. I then identified creation of the `cyberjunkie` account and its addition to the `sudo` group, mapping that persistence behavior to T1136.001. Finally, I traced sudo activity and recovered the exact curl command used to download a script.

The main lesson was that effective SOC investigation comes from correlating authentication, session, account-management and command-execution artifacts into a defensible timeline.

## Interview Questions

### Why was wtmp necessary?
Because the task required the interactive terminal-session timestamp. Authentication and session start are separate events.

### Why is a sudo-enabled new account suspicious?
It provides a persistent privileged identity and can survive remediation of the original compromised credentials.

### Why is the final curl command important?
It proves privileged execution and external script retrieval, providing concrete evidence of post-compromise activity.

### What would you do on a real SOC ticket?
Preserve evidence, contain the affected host/account as appropriate, disable the unauthorized account, review privileged-group membership, investigate the downloaded artifact, hunt for related activity, and document a complete incident timeline.
