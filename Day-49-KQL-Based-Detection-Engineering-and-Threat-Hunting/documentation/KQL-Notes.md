# KQL Notes \| Day 49

## Core Mental Model

``` text
TABLE
  ↓
WHERE
  ↓
EXTEND
  ↓
PROJECT
  ↓
SUMMARIZE
  ↓
ORDER
```

## SPL → KQL

  Splunk SPL           KQL
  -------------------- --------------------------
  `search` / `where`   `where`
  `eval`               `extend`
  `table`              `project`
  `stats`              `summarize`
  `sort`               `sort by` / `order by`
  `dedup`              `distinct` / `summarize`
  `rename`             `project-rename`

## `let`

`let` creates a query-scoped expression or temporary dataset.

``` kusto
let ProcessEvents = datatable(...)
[
    ...
];

ProcessEvents
| where FileName == "powershell.exe"
```

The variable exists only within that query execution.

## `datatable()`

`datatable()` creates inline tabular data. Day 49 used it to model
controlled SOC telemetry without a live Defender or Sentinel tenant.

## Case-Insensitive Matching

The detection uses `in~` for case-insensitive process matching:

``` kusto
InitiatingProcessFileName in~ ("WINWORD.EXE", "EXCEL.EXE")
```

## Detection Principle

Use behavioral context:

``` text
Office parent
    +
PowerShell child
    +
Encoded or hidden execution
```

Network activity is a separate corroborating layer.

## Lab Limitation

The Microsoft public Samples database was used to validate KQL
execution. SOC telemetry was created with `datatable()` and represents
controlled lab data.
