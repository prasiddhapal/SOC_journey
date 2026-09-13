# Day 50 | Active Directory Identity Threat Detection
## Professional SOC Lab Documentation

**Project:** SOC Journey | **Platform:** Splunk | **Status:** COMPLETE
**Domain:** Active Directory / Windows Identity Security / Detection Engineering
**Detection:** Behavioral identity correlation
**Validation:** Controlled synthetic telemetry

---

## 1. Executive Summary
Day 50 moved the SOC Journey from endpoint/process detection into identity-centered threat detection.

Core behavior:
```text
4625 failures → 4624 success → 4728 Domain Admins change → higher-confidence alert
```

Event 4728 records a member added to a security-enabled global group, so actor, group, source, timing, and authorization require investigation. citeturn0search8

**Final controlled validation:** TP=2, TN=5, FP=0, FN=0, **7/7 PASS**.
These metrics apply only to the controlled synthetic dataset.

## 2. Objectives
- Active Directory identity concepts
- Windows authentication investigation
- NTLM and Kerberos context
- Privileged group monitoring
- Identity correlation
- Detection engineering
- False-positive and detection-gap testing
- Detection tuning and regression validation
- Evidence-based SOC reporting

## 3. Windows Identity Telemetry
| Event | Meaning |
|---|---|
| 4624 | Successful logon |
| 4625 | Failed logon |
| 4728 | Member added to security-enabled global group |
| 4740 | Account lockout |
| 4768 | Kerberos TGT request |

Microsoft documents 4624 as successful logon and 4625 as failed logon. citeturn0search0turn0search3
Event 4768 records Kerberos TGT issuance and is not malicious by itself. citeturn0search1

## 4. Detection Hypothesis
> Repeated authentication failures followed by successful authentication and a privileged Domain Admins modification within a bounded period should produce a higher-confidence identity investigation than any individual event.

Required:
```text
4625 >= 3 | 4624 >= 1 | 4728 + Domain Admins >= 1 | duration <= 20 minutes
```
**Severity:** HIGH

## 5. Lab Dataset
```text
datasets/
├── identity_events.csv
├── identity_regression.csv
└── identity_gap_test.csv
```
Contains benign activity, authorized administration, suspicious sequences, privileged changes, and a deliberate Jordan Lee gap-test case.

## 6. Detection Development
The initial implementation used a **10-minute fixed bucket** and missed the slower Jordan Lee sequence.

Jordan Lee:
```text
15:00:11  4625
15:00:19  4625
15:00:27  4625
15:01:02  4624
15:15:44  4728 → Domain Admins
```
Measured duration: **15.55 minutes**.

## 7. Detection Tuning
| Subject | Duration |
|---|---:|
| nathan.brooks | 2.50 min |
| jordan.lee | 15.55 min |

The laboratory threshold was tuned to **20 minutes**. This is a lab validation value, not a universal production threshold.

## 8. Final Detection Logic
```text
failed_auth >= 3
AND successful_auth >= 1
AND privileged_changes >= 1
AND duration_seconds <= 1200
```
`privileged_changes` = EventCode 4728 with `TargetGroup=Domain Admins`.

### Final SPL
```spl
index=main (source="identity_events.csv" OR source="identity_regression.csv" OR source="identity_gap_test.csv") | eval failed_flag=if(EventCode=4625,1,0) | eval success_flag=if(EventCode=4624,1,0) | eval privileged_flag=if(EventCode=4728 AND TargetGroup="Domain Admins",1,0) | stats sum(failed_flag) as failed_auth sum(success_flag) as successful_auth sum(privileged_flag) as privileged_changes min(_time) as first_seen max(_time) as last_seen by SubjectUser | eval duration_seconds=last_seen-first_seen | eval DetectionResult=if(failed_auth>=3 AND successful_auth>=1 AND privileged_changes>=1 AND duration_seconds<=1200,"DETECTED","NOT_DETECTED") | table SubjectUser failed_auth successful_auth privileged_changes duration_seconds DetectionResult
```

## 9. Final Regression
| Subject | Expected | Actual |
|---|---|---|
| adm-domain.admin | NOT_DETECTED | NOT_DETECTED |
| adm-hr.sullivan | NOT_DETECTED | NOT_DETECTED |
| adm-security | NOT_DETECTED | NOT_DETECTED |
| alice.smith | NOT_DETECTED | NOT_DETECTED |
| bob.jones | NOT_DETECTED | NOT_DETECTED |
| jordan.lee | DETECTED | DETECTED |
| nathan.brooks | DETECTED | DETECTED |

**7/7 expected outcomes passed.**

## 10. False-Positive Validation
`adm-domain.admin` performed an authorized `4728 → Domain Admins` change without the preceding `4625 × 3+ → 4624` sequence.

Result: **NOT_DETECTED**.

This demonstrates why atomic `4728 + Domain Admins` detection is noisier than behavioral correlation.
## 11. Investigation Findings
### nathan.brooks
`4625 × 3 → 4624 → 4728 Domain Admins → 4768`
Source: `10.20.30.44` | NTLM | **2.50 min**
**Assessment: High-confidence suspicious identity activity.**
### jordan.lee
`4625 × 3 → 4624 → 4728 Domain Admins`
Source: `10.20.40.55` | NTLM | **15.55 min**
**Assessment: High-confidence suspicious identity activity.**
## 12. Analyst Verdict
> High-confidence suspicious identity activity involving repeated authentication failures, subsequent successful authentication, and a Domain Admins membership modification from the same source context.
Next investigate authorization, account owner, source host, credential activity, group history, privileged logons, Kerberos activity, endpoint activity, and other identities using the source.
The telemetry does **not** independently prove compromise, credential theft, persistence, or malicious intent.
## 13. ATT&CK Mapping
### T1078 | Valid Accounts
Relevant as an analytical mapping for suspicious identity use; it does not prove credential theft or unauthorized account use.
Event 4728 is privilege context, not automatic proof of malicious privilege escalation.
## 14. Detection Engineering Lessons
1. **Single events are weak evidence.** 4624, 4625, 4728, and 4768 can occur legitimately.
2. **Correlation increases confidence:** User + Authentication + Source + Timing + Privilege Change.
3. **Detection gaps must be tested:** Build → Test → Edge Case → Gap → Tune → Regression.
4. **Lab success is not production proof.**
## 15. Production Limitations
The laboratory SPL groups events by `SubjectUser` and measures first-to-last duration.
Production should add true rolling/sequence windows, event ordering, session boundaries, source-host correlation, account/admin baselines, service-account handling, multi-DC considerations, missing/duplicate-event handling, schema normalization, and alert-volume measurement.
Microsoft's Windows Security event collection includes 4624, 4625, 4728, 4740 and 4768 among documented Windows Security events. citeturn0search4
## 16. Evidence
Day 50 contains **13 analyst-captured screenshots** covering baseline, authentication sequence, identity timeline, correlation, regression, false-positive testing, detection-gap testing, duration analysis, 20-minute tuning, and final regression.
## 17. Repository & Workflow
```text
Day-50-Active-Directory/
├── datasets/
├── detections/
├── documentation/
├── evidence/
└── queries/
```
Workflow:
`Prepare → Ingest → Validate → Hunt → Correlate → Test FP → Test Gap → Measure → Tune → Regression → Report`
## 18. Final Status
```text
Day: 50 | Platform: Splunk
Topic: Active Directory Identity Threat Detection
Detection: Authentication → Privilege Correlation
Initial Window: 10 min | Tuned Lab Window: 20 min
Regression: 7/7 PASS | TP/TN: 2/5 | FP/FN: 0/0
Evidence: 13 screenshots | Status: COMPLETE
```
### Final Conclusion
Day 50 demonstrated identity-focused SOC detection engineering through authentication correlation, privileged-group monitoring, false-positive testing, detection-gap discovery, time-window tuning, and regression validation.
> **Good detection engineering is not just making an alert fire. It is proving why it fired, when it should not fire, where it fails, and what the evidence actually supports.**
**SOC Journey | Day 50**
