# SOC Investigation Checklist

## Alert Triage

- [ ] Read the alert carefully.
- [ ] Identify the affected asset.
- [ ] Identify the user.
- [ ] Identify source and destination IPs.
- [ ] Record the initial timestamp.
- [ ] Confirm the timezone.

## SIEM Search

- [ ] Identify the correct index.
- [ ] Search the relevant source.
- [ ] Inspect raw events.
- [ ] Review extracted fields.
- [ ] Narrow the time range.
- [ ] Search related users.
- [ ] Search related hosts.
- [ ] Search related IPs.

## Authentication

- [ ] Check failed attempts.
- [ ] Check successful attempts.
- [ ] Compare source addresses.
- [ ] Check privilege escalation.
- [ ] Check session creation.

## Process Activity

- [ ] Identify suspicious processes.
- [ ] Review command lines.
- [ ] Review hashes.
- [ ] Check parent/child context when available.
- [ ] Correlate process and network activity.

## Network

- [ ] Identify destination.
- [ ] Identify destination port.
- [ ] Identify source port.
- [ ] Check repeated connections.
- [ ] Check DNS context.
- [ ] Check proxy/firewall evidence.

## Timeline

- [ ] Normalise timezones.
- [ ] Sort events chronologically.
- [ ] Identify first suspicious event.
- [ ] Identify follow-on activity.
- [ ] Identify the last known event.

## Evidence

- [ ] Save relevant event details.
- [ ] Record the exact query.
- [ ] Capture required screenshots.
- [ ] Separate facts from assumptions.
- [ ] Verify the final answer.

## Reporting

- [ ] Executive summary
- [ ] Technical evidence
- [ ] Timeline
- [ ] Analysis
- [ ] Impact
- [ ] Conclusion
- [ ] Recommended next steps
