# Correlation Scoring

## Purpose
Use a simple scoring model to prioritize correlated activity for analyst review.

## Inputs
The demonstrated scoring model uses:
- `suspicious`
- `same_user_ip`
- `gap_seconds`

## Example Logic

```spl
| eval correlation_score=
    suspicious
    + same_user_ip
    + if(gap_seconds<=300,1,0)
```

Each satisfied condition contributes one point.

## Score Meaning

### Score 0-1
Limited supporting evidence.

Classification:

`Low Confidence`

### Score 2
Multiple supporting indicators.

Classification:

`Suspicious - Review`

### Score 3
Multiple strong correlation indicators.

Classification:

`High Confidence - Investigate`

## Demonstrated Case
The lab contains:
- Suspicious PowerShell: `1`
- Same user/source: `1`
- Short time gap: `1` when evaluated on the follow-on event

This demonstrates how a correlated event can reach a higher confidence level than a standalone event.

## Important Limitation
This is a learning and detection-engineering model, not a production risk framework.

A real SOC should consider:
- Asset criticality
- Account privilege
- Known-good administrative activity
- Threat intelligence
- Additional process ancestry
- Network activity
- Endpoint evidence
- Historical behavior

## Analyst Principle
Scores should prioritize investigation. They should not replace analyst judgment.

## Outcome
The scoring model provides a transparent explanation for why an event receives a particular investigation priority.
