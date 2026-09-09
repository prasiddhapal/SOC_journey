# 02 - Authentication and Identity Investigation

## Identity Findings
Searches for Nathan Brooks showed authentication activity involving the workstation and domain infrastructure.

Relevant observations included:
- `nathan.brooks` authentication events using NTLM and Kerberos.
- Source addresses included `192.0.2.254` and `10.5.50.12` depending on the authentication flow.
- Domain systems observed included `THM-DC` and `THM-MKT-WS`.

## Group Membership Change
An EventCode `4728` result showed `Nathan Brooks` associated with the `Marketing` group, with `adm-luke.sullivan` appearing as the initiating account in the event fields.

A related EventCode `4737` result showed a modification to the `Marketing` group on `THM-DC`.

### Interpretation
These events establish an authorization/group-change context before the SMB activity. They do not, by themselves, prove malicious privilege escalation. The investigation therefore treats the group change as contextual evidence rather than proof of compromise.
