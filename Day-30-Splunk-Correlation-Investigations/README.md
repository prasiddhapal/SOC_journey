# Day 30 - Splunk Correlation & Investigation

## Objective
Correlate multiple Windows process events in Splunk and turn individual observations into an investigation decision.

## Scenario
The lab uses Windows process telemetry with:
- User: `Administrator`
- Source IP: `10.49.108.48`
- Suspicious PowerShell command: `powershell.exe -EncodedCommand ABC123`
- Follow-on command: `cmd.exe /c whoami`

## Investigation Flow
1. Identify suspicious command indicators.
2. Identify parent-process context.
3. Build a short event timeline.
4. Compare user and source IP across events.
5. Measure the time gap between related events.
6. Calculate a correlation score.
7. Produce an analyst-facing investigation decision.

## Evidence
The PowerShell event contains an encoded-command indicator.
The later `cmd.exe /c whoami` event occurs under the same user and source IP.
The lab data also demonstrates a two-minute gap between the related events.

## Result
The correlation logic classified the activity as **Suspicious - Review** when the correlation score reached `2`.

## Analyst Takeaway
Correlation is stronger than examining a single event in isolation. The goal is not to declare an incident from one keyword, but to connect process context, identity, source, timing, and command behavior.

## Skills Demonstrated
- SPL event construction
- `append`
- `sort`
- `streamstats`
- `eval`
- `match`
- Time-gap analysis
- Evidence correlation
- Investigation decision logic

## Validation
The final search returned both related events and exposed the calculated correlation fields for analyst review.

## Next Step
Continue from correlation into broader alert triage, evidence enrichment, and investigation workflow.
