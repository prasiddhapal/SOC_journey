# 02 — Authentication and Account Activity

## Objective

Investigate SSH authentication and account-management activity using:

```text
/var/log/auth.log
```

## SSH investigation

The logs contained successful and failed SSH authentication events.

A suspicious source address repeatedly attempted authentication against multiple usernames:

```text
10.14.94.82
```

The same log also showed successful SSH authentication from other source addresses, demonstrating why analysts must distinguish failed attempts from successful access.

## Account creation

Account-management entries showed:

```text
useradd: new user name=xerxes
```

followed by:

```text
usermod: add 'xerxes' to group 'sudo'
```

This is significant because creation of a new account followed by membership in a privileged group can indicate persistence or privilege escalation.

## Investigation principle

Correlate:

**authentication → account creation → group membership → subsequent activity**

rather than examining each event in isolation.
