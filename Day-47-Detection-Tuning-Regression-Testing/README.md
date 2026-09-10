# Day 47 | Detection Tuning & Regression Testing
## SOC Analyst Journey | Professional Lab Package

### Purpose
Day 47 validates the Day 46 endpoint detection through controlled regression testing, false-positive testing, edge-case testing, and deliberate detection-gap testing.

### Detection under test
**Office Application → Suspicious PowerShell**

Base behavior:
- Microsoft Word/Excel spawns PowerShell
- Suspicious execution characteristics increase detection confidence
- Process telemetry is the base detection
- Network telemetry is corroborating context, not a mandatory prerequisite

### Primary ATT&CK mapping
- **T1059.001 – PowerShell**

### Engineering objective
Demonstrate that tuning improves coverage without breaking previously validated behavior.

### Evidence standard
The PNG files in `screenshots/` are **professional evidence templates**. They are intentionally labeled as templates and must be reproduced/confirmed in the user's Splunk environment before being treated as live evidence. They do not claim that the pictured queries were executed in Splunk during package generation.

### Day 47 completion criteria
- Baseline preserved
- Benign regression set tested
- Suspicious regression set tested
- Edge cases tested
- Day 46 gap re-tested
- False positives reviewed
- Tuning changes documented
- Regression matrix completed
- Limitations recorded
