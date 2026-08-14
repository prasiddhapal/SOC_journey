# Splunk Basics

Core SPL concepts practiced during the Splunk detection engineering
training.

## Basic Search

Search an index:

```spl
index=main
```

Search for a specific event:

```spl
index=main event_id=4688
```

## `where`

Filter events using conditions.

```spl
index=main
| where event_id=4688
```

Multiple conditions:

```spl
index=main
| where event_id=4688 AND user="Administrator"
```

## `table`

Display selected fields.

```spl
index=main
| table _time host user event_id src_ip process parent pid command
```

## `eval`

Create or calculate a field.

```spl
index=main
| eval suspicious=if(event_id=4688,1,0)
| table _time event_id user suspicious
```

### `if()`

```spl
if(condition, value_if_true, value_if_false)
```

### `case()`

Classify events using multiple conditions.

```spl
index=main
| eval event_type=case(
    event_id=4624, "Successful Logon",
    event_id=4688 AND process="powershell.exe", "PowerShell Execution",
    event_id=4688 AND process="cmd.exe", "CMD Execution",
    true(), "Other"
)
| table _time event_id process event_type
```

## `stats`

Summarize events.

```spl
index=main
| stats count by user
```

Group by multiple fields:

```spl
index=main
| stats count by user event_id
```

### `count()`

Counts events:

```spl
index=main
| stats count by event_id
```

### `dc()`

Counts unique values:

```spl
index=main
| stats dc(src_ip) by user
```

### `values()`

Returns unique values:

```spl
index=main
| stats values(src_ip) by user
```

Combine statistics:

```spl
index=main
| stats count dc(src_ip) values(src_ip) by user
```

## `sort`

Sort results.

Oldest first:

```spl
index=main
| sort _time
```

Newest first:

```spl
index=main
| sort - _time
```

## `head` and `tail`

Return a limited number of results.

```spl
index=main
| sort - _time
| head 10
```

```spl
index=main
| sort _time
| tail 10
```

## `rename`

Rename a field in the results.

```spl
index=main
| stats count by event_id
| rename event_id AS "Windows Event ID"
```

## `fields`

Select fields:

```spl
index=main
| fields _time user event_id process command
```

Remove a field:

```spl
index=main
| fields - host
```

## `dedup`

Keep one result for each unique field value.

```spl
index=main
| dedup user
| table _time user event_id
```

### `stats` vs `dedup`

```text
stats
→ summarizes events

dedup
→ removes duplicate results
```

For example:

```spl
index=main
| stats count by user
```

shows how many events each user generated.

```spl
index=main
| dedup user
```

keeps one result for each unique user.

## `rex`

Extract information from raw text.

```spl
index=main
| rex field=command "(?<program>^[^ ]+)"
| table command program
```

The named capture:

```text
(?<program>...)
```

creates a new field called `program`.

## `eventstats`

Calculate statistics while keeping the original events.

```spl
index=main
| eventstats count by user
| table _time user event_id count
```

Difference:

```text
stats
→ summary results

eventstats
→ original events + calculated statistics
```

## `streamstats`

Calculate values across the event sequence.

Basic previous-event example:

```spl
index=main
| sort _time
| streamstats current=f window=1 last(event_id) as previous_event
| table _time event_id previous_event
```

Concept:

```text
Current Event
     ↓
Previous Event Information
```

### Time Difference

```spl
index=main
| sort _time
| streamstats current=f window=1 last(_time) as previous_time
| eval time_diff=_time-previous_time
| table _time event_id previous_time time_diff
```

This can be used to measure the time between consecutive events.

## `lookup`

Enrich events using a reference dataset.

Concept:

```text
Event
  ↓
Lookup
  ↓
Additional Context
```

Common uses include:

- IP classification
- Asset information
- User information
- Trusted systems
- Threat intelligence

Basic structure:

```spl
| lookup lookup_name matching_field OUTPUT output_field
```

## `mvexpand`

Expand multivalue fields into separate results.

Concept:

```text
[A, B, C]
   ↓
 A
 B
 C
```

Useful when multiple values need to be analyzed individually.

# SOC Investigation Workflow

SPL commands can be combined into an investigation workflow:

```text
Search
  ↓
Filter
  ↓
Select Fields
  ↓
Transform
  ↓
Aggregate
  ↓
Sort / Limit
  ↓
Correlate
  ↓
Investigate
```

Example:

```spl
index=main
| where event_id=4688
| stats count values(process) values(command) by user
| sort - count
| head 10
```

This identifies process-creation activity by user and summarizes the
observed processes and commands.

# Detection Engineering

SPL can also be used to build detection logic.

Example sequence:

```text
4624 Successful Network Logon
        ↓
Privileged User
        ↓
4688 Process Creation
        ↓
PowerShell / CMD
```

The detection should identify activity requiring investigation rather
than automatically declaring the activity malicious.

# Key Reference

| Command | Purpose |
|---|---|
| `where` | Filter events |
| `table` | Display selected fields |
| `eval` | Create or calculate fields |
| `if()` | Conditional logic |
| `case()` | Multiple conditions |
| `stats` | Summarize events |
| `count()` | Count events |
| `dc()` | Count unique values |
| `values()` | Return unique values |
| `sort` | Order results |
| `head` | First N results |
| `tail` | Last N results |
| `rename` | Rename fields |
| `fields` | Select or remove fields |
| `dedup` | Remove duplicate results |
| `rex` | Extract fields from text |
| `eventstats` | Calculate statistics while retaining events |
| `streamstats` | Calculate values across event sequences |
| `lookup` | Enrich events with reference data |
| `mvexpand` | Expand multivalue fields |

## Key Lesson

The goal of SPL is not to memorize commands.

The goal is to turn:

```text
Raw Telemetry
      ↓
Useful Evidence
      ↓
Correlation
      ↓
Detection
      ↓
Investigation
```

into a repeatable SOC workflow.
