# Day 47 Professional Report
## Detection Tuning & Regression Testing

### Executive Summary
Day 47 focuses on validating the Day 46 Office → Suspicious PowerShell detection through structured regression testing. The engineering objective is to improve coverage while preserving benign behavior and previously validated detections.

### Detection Objective
Detect suspicious PowerShell execution originating from Microsoft Office applications using process telemetry. Encoded commands and hidden-window execution are treated as strong contextual signals. Network activity is used as corroborating telemetry rather than a required condition for the base process rule.

### Test Strategy
The regression set covers:
- Known benign administrative activity
- Previously detected suspicious activity
- Hidden PowerShell without encoded execution
- Command-line and executable-path variations
- PowerShell Core (`pwsh.exe`) as a coverage decision
- False-positive review
- Detection-gap validation

### Key Tuning Decision
`-NoProfile` is not treated as malicious by itself because it is common in legitimate automation. The tuned rule instead prioritizes encoded-command and hidden-window behaviors.

### Lab Metrics
The controlled six-case validation set is documented as:
- TP: 3
- TN: 3
- FP: 0
- FN: 0
- Precision: 100%
- Recall: 100%

**Limitation:** This is a tiny controlled lab sample and is not evidence of production detection accuracy.

### Analyst Assessment
The detection should remain experimental until tested against broader telemetry and real organizational workloads. Future improvements should include robust field normalization, PowerShell Core coverage, richer process lineage, signer/path context, and scalable regression automation.

### Evidence Handling
All PNGs in the screenshot directory are labeled templates. They should be replaced by actual Splunk screenshots after the corresponding queries are executed.

### Primary MITRE ATT&CK
T1059.001 — PowerShell

### Final Principle
A detection is an engineering artifact. It requires versioning, regression testing, false-positive analysis, gap testing, and explicit evidence boundaries.
