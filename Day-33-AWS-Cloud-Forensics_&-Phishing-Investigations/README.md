# Day 33

## Overview
Day 33 covered two practical security investigations:

1. **AWSRaid**: AWS CloudTrail investigation using Splunk.
2. **Email Attachment Analysis**: analysis of an HTML phishing attachment, obfuscation, credential capture, and network evidence.

## Labs
- AWSRaid
- Email Attachment Analysis / ParrotPost

## Main Skills
- CloudTrail log investigation
- Splunk SPL filtering and tabulation
- S3 activity analysis
- IAM activity analysis
- HTML/MIME analysis
- Base64 decoding
- JavaScript and CSS obfuscation analysis
- Phishing analysis
- Browser Developer Tools
- HTTP request/response analysis

## Investigation Chains

### AWSRaid
CloudTrail events -> Splunk -> suspicious S3 activity -> public-access/policy investigation -> IAM activity -> persistence investigation.

### Email Attachment
Email attachment -> HTML -> Base64 -> JavaScript decoding -> fake login page -> credential capture -> HTTP request -> credential log.

## Day 33 Outcome
Both labs were completed.

The email-analysis lab produced the flag:
`THM{c4p7ur3d_y0ur_cr3d5}`

## Notes
These documents record the workflow and evidence observed during the labs. Values not directly observed are not inferred.
