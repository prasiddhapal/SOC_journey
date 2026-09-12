# Day 49 \| KQL for SOC Analysts

## Overview

Day 49 translated the detection-engineering workflow from Splunk and
Sigma into Kusto Query Language (KQL).

Covered: - KQL execution environment - KQL fundamentals - Windows
process hunting - Office → PowerShell detection - Encoded and hidden
PowerShell - Network telemetry - Process + network correlation -
False-positive validation - Detection-gap testing - Sigma → KQL
translation - Regression testing - Evidence collection

## Lab Data

The SOC telemetry is controlled synthetic data modeled after
Defender-style endpoint fields. It was executed with KQL `datatable()`
in the Microsoft public Kusto Help cluster.

This is not a live Microsoft Defender or Microsoft Sentinel tenant.

## Final Validation

Seven controlled test cases were evaluated: - 7 passed - 0 failed - 0
false positives - 0 false negatives

The results apply only to the controlled seven-event validation set and
are not production performance metrics.

## Evidence

The evidence consists of screenshots captured from actual KQL execution.
No fabricated or AI-generated execution evidence is included.
