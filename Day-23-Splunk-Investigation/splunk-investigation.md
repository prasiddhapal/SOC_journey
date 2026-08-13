# Day 23 - Splunk Investigation

## Objective

Practice investigating Windows authentication and process activity
using Splunk.

## Investigation Scope

The investigation focused on correlating:

- Windows Event ID 4624
- Windows Event ID 4688
- Source IP
- User account
- Process
- Parent process
- PID
- Command line

## Investigation Flow

4624 Successful Logon
        |
        v
Source IP: 10.49.108.37
        |
        v
Administrator account
        |
        v
4688 powershell.exe
        |
        v
4688 cmd.exe /c whoami

## Conclusion

The activity is suspicious and requires further investigation.

The available evidence alone is not sufficient to classify the
activity as malicious.

Further investigation should include validation of the source IP,
verification of authorized Administrator activity, and additional
endpoint/network telemetry.
