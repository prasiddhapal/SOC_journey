# Day 50 Professional Report | Active Directory Identity Threat Detection

## Objective
Build and validate an identity-focused SOC detection using Windows Security telemetry.

## Detection hypothesis
Repeated authentication failures followed by successful authentication and a Domain Admins membership modification within a bounded period should generate higher-confidence investigative activity than any individual event.

## Telemetry
- 4624: successful logon
- 4625: failed logon
- 4728: member added to a security-enabled global group
- 4768: Kerberos TGT request, contextual
- 4740: account lockout, contextual

## Detection development
The initial 10-minute fixed-bucket approach missed the deliberately slower Jordan Lee sequence. Duration analysis measured that sequence at 15.55 minutes. A 20-minute bounded validation threshold then detected both suspicious cases while excluding the benign privileged-change case.

## Final lab validation
TP=2, TN=5, FP=0, FN=0. Expected outcomes: 7/7 PASS.

These figures describe only the controlled synthetic dataset and are not production accuracy metrics.

## Findings

### nathan.brooks
Three failed NTLM network authentications from 10.20.30.44 were followed by successful authentication, a Domain Admins membership modification, and a subsequent Kerberos TGT request. Assessment: high-confidence suspicious identity activity.

### jordan.lee
Three failed NTLM network authentications from 10.20.40.55 were followed by successful authentication and a Domain Admins membership modification. The sequence lasted 15.55 minutes. Assessment: high-confidence suspicious identity activity and successful detection-gap validation.

## False-positive validation
The benign adm-domain.admin case contains a Domain Admins modification without the preceding failure/success sequence and was correctly NOT_DETECTED. This demonstrates why an atomic 4728 + Domain Admins rule would be noisier than the correlated behavior.

## ATT&CK
Primary analytical mapping: T1078 Valid Accounts. This is contextual and does not prove credential theft or unauthorized account use.

## Analyst verdict
High-confidence suspicious identity activity involving repeated authentication failures, successful authentication, and a Domain Admins membership modification. Escalation is warranted for account validation, source-host investigation, privileged-group review, and authorization confirmation. Available telemetry does not independently confirm full account compromise, persistence, or malicious privilege use.

## Production limitations
The validated lab query uses per-user aggregation across the selected dataset. A production implementation should use a true rolling/sequence window, preserve event ordering, distinguish independent sessions, baseline approved administrators and automation, enrich source context, and validate against historical benign activity.
