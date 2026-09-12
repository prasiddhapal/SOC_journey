# Evidence Manifest \| Day 49

## Evidence Standard

Only screenshots captured from actual lab execution are included. No
fabricated results or AI-generated execution evidence are used.

## Screenshots

### 01-kql-environment-success.png

Successful KQL environment validation using the Microsoft Help Cluster,
Samples database, and `StormEvents | take 10`.

### 02-kql-office-powershell-detection.png

Office → PowerShell suspicious-execution detection returning PIDs 7044,
7196, and 8224.

### 03-kql-network-telemetry.png

Controlled network telemetry showing the expected three records.

### 04-kql-detection-validation.png

Controlled validation showing three detections and four non-detections.

### 05-sigma-to-kql-validation.png

Successful Sigma-to-KQL behavioral translation returning the three
expected detections.

### 06-kql-regression-validation.png

Final seven-case regression test showing all cases as PASS.

## Limitations

The screenshots demonstrate actual query execution and controlled lab
validation. They do not demonstrate live Defender/Sentinel telemetry,
production performance, real-world compromise, or successful payload
execution.
