# Day 48 | Sigma Engineering

## SOC Analyst Journey

**Focus:** Portable detection engineering with Sigma and Splunk  
**Detection:** Microsoft Office → PowerShell → suspicious execution  
**Author:** Prasiddha Pal  
**Date:** 2026-09-11

---

## Executive Summary

Day 48 focused on converting an endpoint detection developed in Splunk into a portable Sigma rule and validating that the converted logic preserves the intended detection behavior.

The lab covered:

1. Sigma CLI installation and environment cleanup
2. Sigma rule schema validation
3. Sigma-to-Splunk conversion
4. Portable field selection
5. Splunk field normalization
6. Detection validation
7. Detection-gap testing
8. Evidence preservation

The final portable Sigma rule passed validation with **0 errors, 0 condition errors, and 0 validation issues**.

---

## Evidence Authenticity

All screenshots in `screenshots/` were supplied by the user during the lab session.

No AI-generated screenshots, fabricated SIEM evidence, or simulated terminal screenshots are included.

The Sigma YAML files are intentionally excluded from this documentation package so they can be added manually from the user's local lab environment.

---

## Detection Concept

```text
Microsoft Office
       |
       v
PowerShell / PowerShell Core
       |
       v
Encoded or Hidden Execution
       |
       v
Investigation / Correlation
```

Network activity is treated as a correlation signal rather than a mandatory condition of the base Sigma detection.

---

## Package Structure

```text
Day-48-Sigma-Engineering-Professional/
├── README.md
├── Day-48-Professional-Report.md
├── Detection-Specification.md
├── Field-Mapping.md
├── Validation-Matrix.csv
├── Evidence-Register.md
├── Reproduction-Steps.md
└── screenshots/
    ├── 01-sigma-cli-and-splunk-backend.png
    ├── 02-sigma-cli-version-and-targets.png
    ├── 03-sigma-rule-validation-success.png
    ├── 04-sigma-to-splunk-conversion.png
    ├── 05-splunk-baseline-detection-results.png
    ├── 06-splunk-hidden-powershell-gap-test.png
    └── 07-portable-sigma-field-mapping-validation.png
```

---

## Manual Additions

Add the authentic files from the local lab when publishing the complete evidence package:

- `day48_office_powershell.yml`
- `day48_office_powershell_v1_lab.yml`
- `day48_office_powershell_portable.yml`
- `day48_office_powershell.spl`
- `day48_office_powershell_portable.spl`

These should be copied directly from the user's lab environment rather than regenerated.
