# 04 | DNS Traffic and C2 Investigation

## Objective

Document the DNS-based investigation and preserve the evidence showing command-and-control information.

## DNS as Security Telemetry

DNS is often one of the earliest sources of network visibility available to a SOC analyst.

Useful fields include:

- Source host
- Query name
- Query type
- Timestamp
- Response
- Response data

The training material used DNS tunneling and beaconing as an example of suspicious activity.

## Practical Finding

The DNS packet inspection showed a response containing a TXT record.

The relevant response data was:

`THM{C2CommandFound}`

This confirmed that the exercise traffic contained command-and-control information within the DNS response.

## Why This Matters

A DNS request may appear harmless when viewed only as a destination lookup. However, repeated queries, unusual subdomains, TXT records, timing patterns, or encoded-looking data can warrant investigation.

DNS analysis should therefore consider both:

- **Metadata:** who queried what, when, and how often
- **Content:** what was actually returned

## Evidence

Primary evidence:

`Screenshots/04-scenario2-dns-c2-flag.png`

## Investigation Workflow

1. Identify the suspicious host.
2. Review DNS query frequency and destinations.
3. Examine query names and record types.
4. Inspect DNS responses.
5. Look for suspicious or encoded content.
6. Correlate DNS activity with endpoint and other network telemetry.
7. Preserve the relevant packet evidence.

## Analyst Takeaway

DNS is not just an infrastructure service. It can also become a communication channel for malicious activity, so DNS telemetry should be included in network monitoring and incident investigations.
