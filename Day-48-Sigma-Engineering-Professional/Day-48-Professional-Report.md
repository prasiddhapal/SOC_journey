# Day 48 | Sigma Engineering

## 1. Objective

Develop and validate a portable Sigma detection for suspicious PowerShell execution initiated by Microsoft Office applications, then convert the rule to Splunk and verify its behavior against controlled lab telemetry.

The objective was not simply to produce valid YAML. The detection needed to survive schema validation, backend conversion, field normalization, and detection-gap testing.

---

## 2. Detection Hypothesis

The detection focuses on the following behavioral chain:

```text
Microsoft Word / Excel
        ↓
PowerShell / PowerShell Core
        ↓
Encoded or hidden execution
```

The base detection identifies suspicious process behavior. Network activity is retained as an investigation and correlation signal rather than being required for the base rule.

### Rationale

PowerShell by itself is common administrative activity.

Office spawning PowerShell is more suspicious.

Office spawning PowerShell with encoded or hidden execution characteristics provides a stronger investigation candidate.

---

## 3. Environment

### Sigma

- Sigma CLI: 3.1.0
- Installation method: pipx
- Splunk backend: installed
- Splunk targets: `splunk`, `splunk_spl2`

### Detection tooling

- Sigma rule validation
- Sigma-to-Splunk conversion
- Splunk SPL validation
- Controlled synthetic telemetry
- Detection-gap testing

---

## 4. Rule Engineering

### Base selections

**Parent process**

- `WINWORD.EXE`
- `EXCEL.EXE`

**Child process**

- `powershell.exe`
- `pwsh.exe`

**Suspicious execution characteristics**

- `-enc`
- `-EncodedCommand`
- `-WindowStyle Hidden`
- `-w hidden`

### Condition

```text
selection_parent
AND
selection_process
AND
selection_suspicious
```

The rule intentionally does not alert on `-NoProfile` alone because that signal is weak and commonly appears in legitimate automation.

---

## 5. Sigma Validation

The final portable rule was checked with the installed Sigma CLI.

Validation result:

```text
Found 0 errors, 0 condition errors and 0 issues.
No rule errors found.
No condition errors found.
No validation issues found.
```

This establishes that the rule passed the installed validator's structural and condition checks.

---

## 6. Sigma → Splunk Conversion

The rule was successfully converted using:

```bash
sigma convert   --target splunk   --pipeline splunk_windows   day48_office_powershell_portable.yml
```

The conversion preserved the intended logical components:

```text
ParentImage
AND
Image
AND
CommandLine
```

The portable version uses `Image` rather than the lab-specific `NewProcessName`.

---

## 7. Telemetry Field Mapping

The synthetic Splunk dataset exposes the child process image as:

```text
NewProcessName
```

The portable Sigma rule uses:

```text
Image
```

For validation, the Splunk search normalized the lab field:

```spl
| eval Image=NewProcessName
```

This is explicitly a **lab-specific schema mapping**. It is not presented as a universal Splunk field definition.

---

## 8. Validation Results

| Test ID | Scenario | Expected | Actual | Result |
|---|---|---|---|---|
| TC01 | Benign Word to PowerShell | NOT_DETECTED | NOT_DETECTED | PASS |
| TC02 | Suspicious Encoded PowerShell | DETECTED | DETECTED | PASS |
| TC03 | Suspicious Encoded PowerShell plus Network | DETECTED | DETECTED | PASS |
| TC04 | Hidden PowerShell without Encoding | DETECTED | DETECTED | PASS |
| TC05 | Portable Sigma field mapping | QUERY_EXECUTES_AND_MATCHES | QUERY_EXECUTES_AND_MATCHES | PASS |

---

## 9. Detection-Gap Test

The gap test deliberately removed encoded execution and used hidden PowerShell:

```text
WINWORD.EXE
    ↓
powershell.exe
    ↓
-NoProfile -WindowStyle Hidden
    ↓
Invoke-WebRequest
```

The test generated PID `8224`.

The portable detection successfully matched the event.

This demonstrates that the detection is not dependent exclusively on encoded PowerShell.

---

## 10. Observed Suspicious Cases

The validated dataset included:

### PID 7044

- Host: `MKT-WS-031`
- User: `nathan.brooks`
- Parent: `WINWORD.EXE`
- Child: `powershell.exe`
- Characteristic: encoded execution

### PID 7196

- Host: `MKT-WS-031`
- User: `nathan.brooks`
- Parent: `WINWORD.EXE`
- Child: `powershell.exe`
- Characteristic: encoded execution
- Network activity was separately associated with the process

### PID 8224

- Host: `MKT-WS-044`
- User: `jordan.lee`
- Parent: `WINWORD.EXE`
- Child: `powershell.exe`
- Characteristic: hidden execution without encoded command
- Network activity was present in the gap-test scenario

These observations demonstrate detection behavior only. They do not, by themselves, establish successful compromise or malicious intent.

---

## 11. Detection Engineering Lessons

### Detection is not the same as response

The Sigma rule identifies behavior suitable for investigation. Containment or automated response requires additional evidence and policy.

### Portable logic still needs schema mapping

A portable detection language does not eliminate differences in telemetry schemas. Field normalization or backend pipelines remain necessary.

### Network is useful corroboration

Network activity increases investigative confidence but should not necessarily be required for the base process detection.

### Validation must include gaps

The hidden-PowerShell test demonstrated why regression and gap testing matter. A detection that only catches one command-line representation is incomplete.

---

## 12. Limitations

- Validation used a small synthetic dataset.
- Results demonstrate lab behavior, not production detection accuracy.
- No production false-positive rate was established.
- The field mapping reflects the synthetic Splunk schema used in this lab.
- Network correlation was validated separately from the base Sigma rule.

---

## 13. Final Assessment

Day 48 successfully progressed from:

```text
Splunk detection
      ↓
Sigma rule
      ↓
Sigma validation
      ↓
Splunk conversion
      ↓
Field mapping
      ↓
Detection validation
      ↓
Gap testing
```

The final portable rule passed validation and reproduced the expected detection behavior in the controlled lab.
