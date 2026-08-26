# 02 - Splunk and CloudTrail

## Useful Base Search

```spl
index="aws_cloudtrail" eventSource="s3.amazonaws.com"
```

## Count Events by API

```spl
index="aws_cloudtrail" eventSource="s3.amazonaws.com"
| stats count by eventName
| sort -count
```

The observed results showed high activity for:
- `PutObject`
- `GetObject`
- `GetBucketAcl`

Other S3 API calls were also present.

## Inspect S3 Bucket Activity

```spl
index="aws_cloudtrail" eventSource="s3.amazonaws.com"
| table _time userIdentity.userName eventName requestParameters.bucketName requestParameters
| sort 0 _time
```

This makes the investigation easier by placing the timestamp, actor, API call, bucket, and parameters together.

## Public Access Investigation

A search for public-access related terms returned `GetAccountPublicAccessBlock` events from multiple users.

The observed usernames included:
- `devops.ethan`
- `helpdesk.luke`
- `appdev.mark`
- `businessanalyst.peter`
- `cloudops.ryan`
- `dataanalyst.sarah`
- `marketing.sophia`

The response values shown for these events were `null` in the displayed table.

## Bucket Policy Status

Search used:

```spl
index="aws_cloudtrail" eventSource="s3.amazonaws.com" eventName="GetBucketPolicyStatus"
| table _time userIdentity.userName requestParameters.bucketName responseElements
| sort 0 _time
```

This showed repeated policy-status checks against several buckets.

## IAM Activity

The investigation also moved to IAM events.

### CreateUser

```spl
index="aws_cloudtrail"
| search eventName="CreateUser"
| table _time userIdentity.userName eventName requestParameters.userName
| sort 0 _time
```

Observed event:
- Actor: `helpdesk.luke`
- Created user: `marketing.mark`
- Time shown: `2023-11-02 09:59:33`

### AddUserToGroup

```spl
index="aws_cloudtrail"
| search eventName="AddUserToGroup"
| table _time userIdentity.userName eventName requestParameters.userName requestParameters.groupName
| sort 0 _time
```

Observed event:
- Actor: `helpdesk.luke`
- User: `marketing.mark`
- Group: `Admins`
- Time shown: `2023-11-02 09:59:38`

## Key Lesson
A good CloudTrail workflow moves from broad event counts to targeted event filtering, then correlates actor, time, API, resource, and request parameters.
