# Day 42 | Active Directory Security & Windows Identity Investigation

**Status:** Completed for today's shortened session  
**Primary focus:** Active Directory, Kerberos, Windows identity telemetry, Kerberoasting indicators, privileged service accounts, evidence correlation.

## Objectives
- Understand Domain Controllers and AD DS
- Explain Kerberos TGT/TGS flow
- Map Event IDs 4768 and 4769
- Understand SPNs and Kerberoasting
- Investigate privileged service-account use
- Correlate 4624, 4672, 4688 and 4769
- Apply evidence → observation → hypothesis → confidence → response

## Key findings
- 4768 → Kerberos authentication-service/TGT request
- 4769 → Kerberos service-ticket/TGS request
- Kerberoasting can involve TGS requests for SPN-backed service accounts followed by offline cracking
- RC4 is a higher-risk contextual signal, not proof by itself
- Privileged service accounts create significant blast radius if compromised
- Correlation is required before declaring compromise

## Mini-case
09:41:12  4624  svc_backup  Source 10.10.20.55  Logon Type 10
09:41:14  4672  svc_backup  Special privileges assigned
09:42:03  4688  svc_backup  powershell.exe  Parent cmd.exe
09:43:21  4769  svc_backup  CIFS/FILE-02  RC4

Context: 10.10.20.55 belongs to a finance employee and had not previously used svc_backup.

## Analyst assessment
Evidence: Same privileged account across logon, privilege, process and service-ticket telemetry.

Observation: A privileged service account was used from an unusual workstation, followed by PowerShell execution and an RC4 service-ticket request.

Hypothesis: Possible credential compromise, potentially involving Kerberoasting.

Confidence: Medium-High.

Next steps: Isolate the workstation, rotate/reset the credential, invalidate active sessions/tickets as appropriate, investigate endpoint artifacts, scope other uses of the account, and review unnecessary privilege.

## Core lesson
A single authentication event rarely proves an attack. Context and correlation make the difference.
