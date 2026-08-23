# Investigation Decision

## Purpose
Convert correlated evidence into an analyst-facing decision without relying on a single suspicious keyword.

## Decision Inputs
The lab evaluates:
- Suspicious command indicator
- Same user
- Same source IP
- Temporal proximity
- Correlation score

## Correlation Score
The demonstrated logic uses:

```spl
| eval correlation_score=
    suspicious
    + same_user_ip
    + if(gap_seconds<=300,1,0)
```

The score represents supporting evidence, not a definitive incident verdict.

## Decision Logic

```spl
| eval investigation_decision=case(
    correlation_score>=3,"High Confidence - Investigate",
    correlation_score=2,"Suspicious - Review",
    true(),"Low Confidence"
)
```

## Observed Result
For the demonstrated two-event scenario:
- Suspicious indicator: `1`
- Same user/source: `1`
- Time gap within five minutes: `1` when available

The investigation logic can therefore escalate the classification when all supporting conditions are present.

## Analyst Reasoning
The correct question is not:

> Is PowerShell suspicious?

Instead:

> What evidence connects this PowerShell activity to the surrounding activity?

That distinction prevents simplistic detection logic.

## Investigation Outcome
The lab produced `Suspicious - Review` for the validated two-event correlation case.

## Operational Principle
Detection logic should support analyst decisions. It should expose the evidence behind the score so that an analyst can validate the result instead of blindly trusting a label.
