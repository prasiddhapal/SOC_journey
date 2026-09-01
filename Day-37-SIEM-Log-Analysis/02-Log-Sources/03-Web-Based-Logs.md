# 03 - Web-Based Log Sources

## Overview

Web applications and supporting infrastructure generate logs that can be collected into a SIEM.

## Common Sources

- Web servers
- WAFs
- API gateways
- Web applications
- CDN infrastructure
- Load balancers

## SQL Injection

Web and WAF logs can provide evidence of suspicious requests associated with SQL injection attempts.

## Web Shells

Web-server telemetry can help investigate suspected web-shell exploitation.

## Application Logs

Application logs may provide context that is not visible from a network connection alone.

## Load Balancer Logs

Load balancers can provide information about requests reaching application infrastructure.

## CDN Logs

CDN telemetry can provide visibility into requests passing through edge infrastructure.

## Analyst Questions

When investigating web activity, ask:

1. What source IP made the request?
2. Which application received it?
3. What URI was requested?
4. What HTTP method was used?
5. What response occurred?
6. Was the request repeated?
7. Did host telemetry show follow-on activity?

## Correlation

A suspicious web request should be correlated with:

- Web-server logs
- WAF logs
- Host process logs
- Authentication events
- Network connections

This helps determine whether the request was only an attempt or resulted in further activity.
