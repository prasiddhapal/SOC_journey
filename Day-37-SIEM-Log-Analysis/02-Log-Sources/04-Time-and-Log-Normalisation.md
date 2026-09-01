# 04 - Time and Log Normalisation

## Time Pitfalls

Time is one of the easiest ways to make an investigation wrong while still looking convincing.

Logs can originate from different time zones.

Some logs use UTC.

Some use local time.

Some may not specify a timezone.

## Example

Suppose the analyst works in UTC-2.

The SIEM may display an event at 9 PM.

A source may record the same event at 7 PM UTC.

These can represent the same moment.

## Investigation Rule

Always determine:

- Source timezone
- SIEM timezone
- Display timezone
- Timestamp format

## Log Normalisation

Different systems can use different formats.

Examples include:

- JSON
- XML
- Plain text

Even when the format is similar, field names may differ.

One source might call a field `src_ip`.

Another might use `source_ip`.

Another might use a nested JSON structure.

## Why Normalise?

Normalisation gives analysts a consistent representation.

Benefits include:

- Easier searching
- Easier filtering
- Easier correlation
- Consistent field names
- More reliable analytics

## Analyst Principle

Do not interpret timestamps until their context is understood.

Do not compare raw field names across sources without understanding how the SIEM parsed them.
