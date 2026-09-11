# Field Mapping

## Purpose

Document the difference between the portable Sigma field model and the synthetic Splunk telemetry used for validation.

| Sigma Field | Lab Splunk Field |
|---|---|
| `ParentImage` | `ParentImage` |
| `Image` | `NewProcessName` |
| `CommandLine` | `CommandLine` |

## Splunk Normalization

```spl
| eval Image=NewProcessName
```

The normalized field is then used by the converted detection logic.

## Scope

This mapping describes the schema used by the Day 48 synthetic dataset.

It does not claim that all Splunk environments use `NewProcessName` for the child process image.

## Engineering Principle

Keep detection logic portable and handle telemetry-specific naming through field mappings or backend pipelines.
