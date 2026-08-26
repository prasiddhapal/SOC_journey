# 06 - Key Findings

## Day 33 Summary

Day 33 combined cloud forensics with email/phishing analysis.

## AWSRaid Findings

### Initial Access
The compromised account identified during the investigation was:

`helpdesk.luke`

### CloudTrail Investigation
Splunk was used to:
- count CloudTrail events
- identify high-volume API calls
- correlate users with timestamps
- inspect S3 buckets and request parameters
- investigate public-access controls
- identify IAM changes

### Notable IAM Activity
Observed activity included:

```text
CreateUser
AddUserToGroup
```

The observed actor was `helpdesk.luke`.

The created user was:

`marketing.mark`

The user was added to:

`Admins`

This is significant because creation of a new user followed by membership in an administrative group can represent a persistence or privilege-related mechanism.

### S3 Investigation
S3 activity included object access and security-configuration APIs such as:
- `GetObject`
- `PutObject`
- `GetBucketAcl`
- `GetBucketPolicyStatus`
- `GetAccountPublicAccessBlock`
- `GetBucketPublicAccessBlock`

## Email Analysis Findings

### Attack Chain

```text
Email
 -> HTML attachment
 -> Base64
 -> JavaScript decoding
 -> Fake login page
 -> Credential capture
 -> HTTP GET
 -> cred-capture.php
 -> creds.txt
```

### Indicators
- `ParrotPostACTIONREQUIRED.htm`
- `atob()`
- `document.write()`
- `XMLHttpRequest`
- `evilparrot.thm:8080`
- `/cred-capture.php`
- `/creds.txt`

### Confirmed Flag

```text
THM{c4p7ur3d_y0ur_cr3d5}
```

## Lessons Learned

1. Start CloudTrail analysis broadly, then narrow by API and actor.
2. Investigate configuration APIs, not just data-access APIs.
3. Treat HTML attachments as potentially executable browser content.
4. Decode obfuscation layer by layer.
5. Use browser Developer Tools to verify actual network behavior.
6. A fake error message can hide successful credential transmission.
7. Correlate timestamps, actors, resources, and actions rather than analyzing events in isolation.

## Completion
- AWSRaid: completed
- Email Attachment Analysis: completed
- Day 33: completed
