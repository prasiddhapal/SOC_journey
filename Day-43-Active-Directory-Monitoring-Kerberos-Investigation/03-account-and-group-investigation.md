# 03 | Account & Group Investigation

Account creation:
`nathan.brooks` was created by `adm-luke.sullivan`.

Group membership:
`nathan.brooks` was added to `Marketing` by `adm-luke.sullivan`.

The Member_Account_Name field uses a distinguished-name representation in group events, so substring matching was required.

Relevant event IDs:
4720 = account created
4722 = account enabled
4724 = password reset attempted
4725 = account disabled
4740 = account locked out
4728 / 4732 / 4756 = security-group membership changes
5136 = directory-service object modification
