# Day 44 | Active Directory Threat Hunting & Kerberos Anomaly Validation

Platform: TryHackMe - Monitoring Active Directory
Tool: Splunk
Status: Complete

## Objective
Proactively hunt for suspicious Kerberos behavior using baselines, rare-value analysis, identity/source correlation, and follow-up endpoint/authentication checks.

## Verified findings
- 38 total Event 4769 records in the initial hunt.
- 29 non-computer-account 4769 records after filtering computer accounts.
- 13 one-time human-account/service pairs.
- Nathan had 8 TGS requests, all from `::ffff:10.5.50.12`.
- `192.0.2.254` appeared across multiple users and was not suitable for Nathan-specific attribution.
- No Event 4771 records were found for Nathan.
- No Event 4688 records were found for Nathan.

## Final assessment
Nathan's activity is more consistent with normal onboarding/resource access than confirmed Kerberos abuse in this dataset. The investigation reduced the initial suspicion rather than forcing a malicious conclusion.

## Hunting model
Baseline -> Hypothesis -> Query -> Anomaly -> Correlation -> Confidence -> Conclusion

## Evidence
Screenshots contain only Splunk query/result evidence from today's practical investigation. No TryHackMe task/instruction screenshots are included.
