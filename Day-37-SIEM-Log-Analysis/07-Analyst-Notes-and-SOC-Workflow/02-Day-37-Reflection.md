# Day 37 Reflection

## What I Practised

Day 37 connected SIEM theory with practical investigation.

I worked through the role of different log sources.

I reviewed host-based telemetry.

I reviewed network-based telemetry.

I reviewed web-based telemetry.

I studied time pitfalls.

I studied log normalisation.

I used Splunk searches to investigate security events.

## Splunk

The practical work reinforced the importance of searching the correct index.

It also reinforced the value of inspecting fields rather than relying only on raw text.

The Linux investigation used authentication logs.

The sudo investigation showed how privileged activity can be reconstructed from events.

Windows searches demonstrated how process and network fields can be combined.

## Active Directory

The Active Directory work introduced Event ID 4768.

The investigation requires reading event fields carefully.

The lab specifically uses pre-authentication type `0` and encryption type `0x17`.

The final account and timestamp are still pending manual verification.

## Lessons Learned

### 1. Evidence First

Do not guess an answer.

Read the event.

### 2. Context Matters

One event rarely provides the complete story.

### 3. Time Matters

Timezone differences can change the apparent order of events.

### 4. Queries Matter

A good query reduces noise and exposes useful fields.

### 5. Documentation Matters

A professional investigation should be reproducible by another analyst.

## Next Session

Continue the unfinished Active Directory investigation.

Open the evidence.

Locate the matching Event ID 4768 event.

Extract the account.

Extract the exact timestamp.

Document the evidence.

Then mark the lab complete.
