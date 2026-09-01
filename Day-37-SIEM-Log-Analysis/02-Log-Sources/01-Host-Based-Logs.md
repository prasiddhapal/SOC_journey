# 01 - Host-Based Log Sources

## Overview

Host-based logs originate from individual systems.

Typical examples are workstations and servers.

## Activity Monitoring

The learning material groups host activity into several areas.

### Authentication

Useful for detecting:

- Brute-force attempts
- Unusual successful logins
- Suspicious authentication behaviour

### Account Management

Useful for identifying:

- Account changes
- Privilege-related changes
- Suspicious account manipulation

### System Events

Useful for understanding changes and activity occurring on a system.

### Process Auditing

Useful for investigating executable and script activity.

This is particularly important when investigating malicious process execution.

### Object Access

Useful when investigating access to sensitive resources.

### Policy Changes

Useful for identifying changes that may affect security controls.

## Analyst Perspective

Host logs answer:

"What happened on this machine?"

The answer becomes stronger when host activity is correlated with authentication and network data.

## Practical Rule

Record the host, user, process, command line, timestamp, and relevant event identifier whenever those fields are available.
