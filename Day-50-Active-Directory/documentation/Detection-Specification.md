# Detection Specification

## Name
Authentication Failure -> Success -> Domain Admins Modification

## Required conditions
- EventCode 4625 >= 3
- EventCode 4624 >= 1
- EventCode 4728 with TargetGroup=Domain Admins >= 1
- first-to-last observed duration <= 20 minutes

## Severity
HIGH

## False positives
- Authorized privileged administrators
- IAM automation
- Helpdesk workflows
- Emergency access procedures
- Approved provisioning/role assignment

## Contextual events
4768 and 4740 provide context and should not independently trigger this primary detection.

## Production requirement
Replace the lab aggregate-duration method with a true rolling/sequence correlation implementation.
