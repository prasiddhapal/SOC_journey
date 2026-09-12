# Day 49 Field Mapping

## Purpose

Document the relationship between vendor-neutral Sigma concepts and the
controlled KQL schema.

  Detection Concept    Sigma Field     KQL Lab Field
  -------------------- --------------- -----------------------------
  Parent process       `ParentImage`   `InitiatingProcessFileName`
  Child process        `Image`         `FileName`
  Command line         `CommandLine`   `ProcessCommandLine`
  Process identifier   Process ID      `ProcessId`
  Account              User            `AccountName`
  Host                 Host            `DeviceName`

## Limitation

The Day 49 dataset is controlled synthetic telemetry modeled after
Defender-style endpoint fields. It is not a live Microsoft Defender
Advanced Hunting dataset.

## Translation

Sigma detection intent was preserved while the field names were mapped
to the Day 49 KQL schema.

Portable detection logic does not imply identical telemetry field names
across platforms.
