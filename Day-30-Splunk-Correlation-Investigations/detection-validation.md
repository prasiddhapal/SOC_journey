# Detection Validation

## Purpose
Validate that the correlation search produces the expected fields and classification.

## Test Data
The lab creates two controlled events.

### Positive Indicator
```text
powershell.exe -EncodedCommand ABC123
```

Expected:
- `suspicious=1`

### Related Follow-On Activity
```text
cmd.exe /c whoami
```

Expected:
- Related user
- Related source IP
- Measurable time gap

## Validation Fields
The final search exposes:

```text
_time
user
src_ip
parent
process
pid
command
suspicious
parent_risk
previous_time
gap_seconds
same_user_ip
correlation_score
investigation_decision
```

## Validation Result
The search returned both test events.

The suspicious PowerShell event was identified correctly.

The follow-on `cmd.exe` event was retained in the same timeline.

The time gap was calculated as `120` seconds in the demonstrated test.

The same-user/source-IP condition evaluated as `1`.

## Expected Classification
The demonstrated correlation logic produced:

`Suspicious - Review`

## Why Validation Matters
A detection is not complete because SPL runs without an error.

The analyst must verify:
- Detection condition
- Context fields
- Calculated values
- Classification
- Expected output

## False-Positive Consideration
`cmd.exe /c whoami` is not automatically malicious.
PowerShell is not automatically malicious either.

The detection becomes more meaningful when multiple contextual indicators align.

## Conclusion
The controlled test confirms that the correlation pipeline is functioning as designed.
