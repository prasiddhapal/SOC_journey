# Reproduction Steps

## 1. Verify Sigma

```bash
which sigma
sigma version
sigma list targets
sigma plugin list | grep -i splunk
```

Expected environment:

```text
Sigma CLI 3.1.0
Splunk backend installed
```

## 2. Validate the portable rule

```bash
cd ~/Documents/lab
sigma check day48_office_powershell_portable.yml
```

Expected:

```text
Found 0 errors, 0 condition errors and 0 issues.
```

## 3. Convert to Splunk

```bash
sigma convert   --target splunk   --pipeline splunk_windows   day48_office_powershell_portable.yml
```

## 4. Normalize the lab telemetry

```spl
| eval Image=NewProcessName
```

Then evaluate the converted logic against the normalized process image field.

## 5. Validate the detection

Test:
- benign Office → PowerShell
- encoded PowerShell
- encoded PowerShell plus network
- hidden PowerShell without encoding
- portable field mapping

## 6. Preserve evidence

Keep authentic screenshots and original rule/query files from the lab. Do not replace live evidence with generated images.
