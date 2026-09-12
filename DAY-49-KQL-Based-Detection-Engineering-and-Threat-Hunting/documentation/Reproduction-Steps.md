# Day 49 Reproduction Steps

## 1. Enter the Lab Directory

``` bash
cd ~/Documents/lab/Day-49-KQL
```

## 2. Verify Structure

``` bash
tree ~/Documents/lab/Day-49-KQL
```

Expected query files:

``` text
queries/
├── 01_kql_basics.kql
├── 02_process_hunting.kql
├── 03_office_powershell.kql
├── 04_process_network_correlation.kql
└── 05_sigma_to_kql.kql
```

## 3. Validate KQL Environment

Connect to:

``` text
https://help.kusto.windows.net
```

Select the `Samples` database and run:

``` kusto
StormEvents
| take 10
```

Expected: 10 records.

## 4. Run KQL Fundamentals

Execute the examples in `01_kql_basics.kql`: - `where` - `project` -
`extend` - `summarize` - `sort`

## 5. Process Hunting

Run the controlled process query and filter:

``` kusto
| where FileName == "powershell.exe"
```

Expected: 7 records.

## 6. Office → PowerShell Detection

Apply the detection conditions for Office parent, PowerShell child, and
encoded or hidden execution.

Expected detections:

``` text
7044
7196
8224
```

## 7. Network Telemetry

Execute the controlled network dataset.

Expected:

``` text
4120 → 10.20.0.10:389
7196 → 185.174.175.187:443
8224 → 203.0.113.50:443
```

## 8. Process + Network Correlation

Correlate host and process identifier.

Expected higher-confidence cases:

``` text
7196
8224
```

## 9. Sigma → KQL

Run `05_sigma_to_kql.kql`.

Expected:

``` text
7044
7196
8224
```

## 10. Regression

Expected:

``` text
4120  NOT_DETECTED  PASS
5236  NOT_DETECTED  PASS
6112  NOT_DETECTED  PASS
7044  DETECTED      PASS
7196  DETECTED      PASS
8224  DETECTED      PASS
8301  NOT_DETECTED  PASS
```

## 11. Validation Metrics

For the controlled dataset:

``` text
TP = 3
TN = 4
FP = 0
FN = 0
```

These metrics are limited to the seven-event synthetic validation set.
