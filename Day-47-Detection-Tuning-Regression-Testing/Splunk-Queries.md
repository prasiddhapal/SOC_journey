# Day 47 Splunk Query Pack

## Baseline
```spl
source="day46_detection_validation.csv"
| dedup extracted_Host ProcessId
| search ParentImage="*WINWORD.EXE" NewProcessName="*powershell.exe"
| table Time extracted_Host User ParentImage NewProcessName CommandLine ProcessId Scenario
```

## Tuned detection
```spl
index=main
| search ParentImage="*WINWORD.EXE" NewProcessName="*powershell.exe"
| search CommandLine="*-enc*"
    OR CommandLine="*-EncodedCommand*"
    OR CommandLine="*-WindowStyle Hidden*"
    OR CommandLine="*-w hidden*"
| eval detection="Office → Suspicious PowerShell"
| eval severity="HIGH"
| eval mitre_technique="T1059.001"
| table _time extracted_Host User ProcessId CommandLine detection severity mitre_technique
```

## Hunt for Office → PowerShell without suspicious switch
```spl
index=main
| search ParentImage="*WINWORD.EXE" OR ParentImage="*EXCEL.EXE"
| search NewProcessName="*powershell.exe" OR Image="*powershell.exe"
| table _time extracted_Host User ParentImage NewProcessName CommandLine ProcessId
```

## Gap test
```spl
index=main
| search ParentImage="*WINWORD.EXE" NewProcessName="*powershell.exe"
| search CommandLine="*Invoke-WebRequest*"
| table _time extracted_Host User ProcessId CommandLine
```

## Destination pivot
```spl
index=main
| search DestinationIp="185.174.175.187"
| dedup extracted_Host ProcessId DestinationIp DestinationPort
| stats count values(extracted_Host) as Hosts
        values(User) as Users
        values(ProcessId) as PIDs
        values(Image) as Processes
        values(SourceIp) as SourceIPs
        by DestinationIp DestinationPort
```

## Lab confusion matrix
```spl
| makeresults
| eval TP=3,TN=3,FP=0,FN=0
| eval Precision=round(TP/(TP+FP)*100,1)
| eval Recall=round(TP/(TP+FN)*100,1)
| table TP TN FP FN Precision Recall
```

### Field note
Field names vary by data source. `extracted_Host` reflects the Day 46 lab ingestion behavior where CSV `Host` conflicted with Splunk's reserved host field.
