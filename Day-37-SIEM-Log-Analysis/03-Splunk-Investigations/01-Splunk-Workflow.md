# 01 - Splunk Investigation Workflow

## Investigation Method

The practical work used Splunk to search task-specific indexes.

A repeatable workflow prevents random searching.

## Step 1 - Identify the Index

Example:

```spl
index=task5
```

## Step 2 - Search Broadly

Example:

```spl
index=task5 search sudo
```

This provides a starting point for locating sudo-related events.

## Step 3 - Inspect Fields

Useful fields observed during the investigation included:

- `host`
- `source`
- `sourcetype`
- `action`
- `COMMAND`
- `process`
- `user`

## Step 4 - Narrow the Search

Use specific values after identifying the structure of the events.

## Step 5 - Build a Timeline

Order events by timestamp.

Look for:

- Failed authentication
- Successful authentication
- Privilege escalation
- Process execution
- Network activity

## Step 6 - Correlate

Use common identifiers such as:

- Username
- Host
- IP address
- Process
- Timestamp

## Step 7 - Document

Record:

- Query
- Event
- Timestamp
- Interpretation
- Supporting evidence

## Principle

A query is a method of finding evidence.

It is not itself proof of intent.
