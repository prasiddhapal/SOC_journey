# 01 - SIEM Fundamentals

## 1. Purpose

A Security Information and Event Management platform centralises security-relevant logs.

The purpose is to make security data available for analysis and correlation.

## 2. Centralised Visibility

An organisation can have many sources.

Examples include:

- Workstations
- Servers
- Network devices
- Cloud services
- Identity providers
- Applications

Investigating every source independently is inefficient.

A SIEM provides a common location for analysis.

## 3. Correlation

Correlation connects events that may originate from different systems.

For example:

1. A user authenticates.
2. The same account performs a privileged action.
3. A process executes.
4. A network connection follows.

Looking at these events together provides more context.

## 4. Historical Analysis

Historical data allows an analyst to search backwards.

This is useful when determining whether an event is isolated or part of a pattern.

## 5. SOC Workflow

A basic workflow is:

1. Alert arrives.
2. Analyst validates the event.
3. Analyst searches related logs.
4. Analyst identifies supporting evidence.
5. Analyst builds a timeline.
6. Analyst determines likely activity.
7. Analyst documents the result.

## 6. Key Principle

The SIEM is not the investigation itself.

It is the central source of telemetry used by the analyst.

The quality of the investigation depends on how the analyst searches, correlates, validates, and documents the evidence.
