# 09 - Day 41 Interview Practice

## Technical
1. What does Windows EventCode 5145 tell a SOC analyst?
2. Why is `WriteData (or AddFile)` more meaningful than merely seeing a share access event?
3. Why should EventCode 5145 be correlated with authentication and endpoint telemetry?
4. Why does temporal proximity between a process and a file operation not prove causation?
5. What additional telemetry would improve process-to-file attribution?

## Scenario
An analyst sees `Notepad.exe` one second before a network-share write. The analyst says, "Notepad wrote the file." What is wrong with that conclusion?

Expected reasoning: the evidence establishes correlation but not direct causation. A direct file telemetry or EDR relationship is required for high-confidence attribution.

## HR/Communication
Explain the incident to a non-technical manager without claiming that an unconfirmed action was malicious.
