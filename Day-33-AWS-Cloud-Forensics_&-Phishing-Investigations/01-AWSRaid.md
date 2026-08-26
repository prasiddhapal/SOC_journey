# 01 - AWSRaid

## Objective
Investigate AWS CloudTrail activity in Splunk to identify unauthorized access, configuration changes, and persistence mechanisms.

## Environment
- Index: `aws_cloudtrail`
- Tool: Splunk Search & Reporting
- Log source: AWS CloudTrail

## Initial Compromise
The investigation identified the compromised account as:

`helpdesk.luke`

The lab question asked for the username of the compromised user, and the observed result was `helpdesk.luke`.

## S3 Activity
A CloudTrail search for S3 activity showed repeated operations including:

- `PutObject`
- `GetObject`
- `GetBucketAcl`
- `GetBucketPublicAccessBlock`
- `GetBucketPolicyStatus`
- `ListAccessPoints`
- `HeadBucket`
- `GetStorageLensDashboardDataInternal`
- `GetStorageLensConfiguration`
- `ListBuckets`
- `ListObjects`
- `GetBucketOwnershipControls`
- `GetBucketVersioning`
- `GetAccountPublicAccessBlock`
- `HeadObject`
- `GetBucketCors`
- `GetBucketObjectLockConfiguration`
- `GetBucketPolicy`
- `GetObjectTagging`
- `CreateBucket`

## Important Observation
The S3 investigation showed access to multiple buckets, including names associated with:

- legal documents
- marketing assets
- research project files
- customer-data backups
- contracts
- product designs
- backup and restore
- CloudTrail logs

## Investigation Direction
The repeated access to S3 objects and bucket configuration APIs made S3 permissions and public-access controls important areas to investigate next.

## Key Lesson
Do not look only for obvious data access. CloudTrail configuration APIs can reveal attempts to understand or weaken security controls.
