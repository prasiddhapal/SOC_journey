# Day 49 Professional Report \| KQL for SOC Analysts

## 1. Executive Summary

Day 49 focused on Kusto Query Language (KQL) for SOC detection and
threat hunting. The goal was to reproduce the behavioral detection
developed during the earlier Splunk and Sigma work using KQL.

The lab progressed from KQL fundamentals into endpoint process
detection, network correlation, Sigma-to-KQL translation, and regression
testing.

## 2. Objectives

1.  Establish a working KQL execution environment.
2.  Learn core KQL operators.
3.  Model controlled endpoint telemetry.
4.  Hunt PowerShell activity.
5.  Detect Microsoft Office spawning suspicious PowerShell.
6.  Correlate suspicious process activity with network telemetry.
7.  Validate benign and suspicious scenarios.
8.  Translate Sigma logic into KQL.
9.  Perform regression testing.
10. Preserve reproducible evidence.

## 3. Execution Environment

KQL execution was validated using the Microsoft public Kusto Help
cluster and the Samples database.

Environment test:

``` kusto
StormEvents
| take 10
```

The query completed successfully and returned 10 records.

The SOC dataset was created inside queries with `datatable()` and `let`.
This avoids claiming that the controlled lab data was live Defender or
Sentinel telemetry.

## 4. KQL Fundamentals

The following operators were executed successfully: - `where` for
filtering - `project` for field selection - `extend` for calculated
fields - `summarize` for aggregation - `sort` for ordering

## 5. Detection Hypothesis

``` text
Microsoft Office
      ↓
PowerShell
      ↓
Encoded OR hidden execution
      ↓
Detection
```

Network activity was treated as corroborating evidence rather than a
prerequisite for the base process detection.

## 6. Controlled Process Telemetry

Seven process events were tested:

  ------------------------------------------------------------------------
                    PID Host             Scenario         Expected
  --------------------- ---------------- ---------------- ----------------
                   4120 FIN-WS-014       Benign Word to   NOT_DETECTED
                                         PowerShell       

                   5236 HR-WS-022        Benign Excel     NOT_DETECTED
                                         administrative   
                                         script           

                   6112 FIN-WS-019       Benign Word to   NOT_DETECTED
                                         PowerShell       

                   7044 MKT-WS-031       Suspicious       DETECTED
                                         Encoded          
                                         PowerShell       

                   7196 MKT-WS-031       Suspicious       DETECTED
                                         Encoded          
                                         PowerShell plus  
                                         Network          

                   8224 MKT-WS-044       Gap Test Hidden  DETECTED
                                         PowerShell plus  
                                         Network          

                   8301 FIN-WS-014       Benign Word      NOT_DETECTED
                                         PowerShell       
                                         variation        
  ------------------------------------------------------------------------

## 7. Detection Logic

The KQL detection required an Office parent, a PowerShell child, and
encoded or hidden execution characteristics.

``` kusto
| where InitiatingProcessFileName in~ ("WINWORD.EXE", "EXCEL.EXE")
| where FileName in~ ("powershell.exe", "pwsh.exe")
| where ProcessCommandLine contains "-enc"
    or ProcessCommandLine contains "-EncodedCommand"
    or ProcessCommandLine contains "-WindowStyle Hidden"
    or ProcessCommandLine contains "-w hidden"
```

The detection returned PIDs 7044, 7196, and 8224.

`-NoProfile` alone was intentionally not treated as malicious.

## 8. Network Correlation

Network events included: - PID 4120 → `10.20.0.10:389` - PID 7196 →
`185.174.175.187:443` - PID 8224 → `203.0.113.50:443`

Process and network telemetry were correlated by host and process
identifier.

The higher-confidence correlated cases were: - PID 7196 - PID 8224

Correlation does not independently prove compromise, successful payload
retrieval, persistence, or malicious intent.

## 9. Sigma → KQL Translation

The Day 48 Sigma behavior was reproduced in KQL.

  Sigma Concept   KQL Lab Field
  --------------- ---------------------------
  ParentImage     InitiatingProcessFileName
  Image           FileName
  CommandLine     ProcessCommandLine
  Process ID      ProcessId
  User            AccountName
  Host            DeviceName

The behavioral logic was preserved while mapping the schema to the
controlled KQL dataset.

## 10. Regression Testing

Final regression results:

``` text
Test cases:       7
Passed:           7
Failed:           0
False positives:  0
False negatives:  0
```

For the controlled dataset:

``` text
TP = 3
TN = 4
FP = 0
FN = 0
```

This equals 100% precision and 100% recall only for this seven-event
synthetic validation set. It must not be represented as production
accuracy.

## 11. Key Engineering Lessons

1.  KQL queries require a database context.
2.  `let` creates query-scoped expressions or temporary datasets.
3.  Detection should focus on behavior and context rather than isolated
    strings.
4.  Network telemetry can increase confidence without being required by
    the base detection.
5.  Sigma portability still requires telemetry-schema mapping.
6.  Case-insensitive process matching can improve robustness.
7.  Benign validation is essential.
8.  Detection changes require regression testing.
9.  Lab metrics do not represent production performance.
10. Evidence must distinguish actual execution from modeled telemetry.

## 12. Final Assessment

Day 49 demonstrated the ability to execute KQL, hunt process telemetry,
build behavioral detections, correlate process and network activity,
translate Sigma logic into KQL, validate expected outcomes, and perform
regression testing.

This extends the detection-engineering progression from Splunk to Sigma
to KQL.
