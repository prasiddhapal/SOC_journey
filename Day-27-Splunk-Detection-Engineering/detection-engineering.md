# Day 27 - Detection Engineering
## Objective
Build a Splunk detection using authentication (`4624`), process creation (`4688`), time correlation, PowerShell indicators, and parent-process context.

## Detection Flow

```text
4624 → 4688 → ≤300 seconds → PowerShell → Risk → Severity
```

## Core Events

```text
4624 = Successful Authentication
4688 = Process Creation
```

Lab chain:

```text
explorer.exe → powershell.exe → cmd.exe
```

## Authentication Correlation

```spl
| eval auth_time_marker=if(event_id=4624,_time,null())
| eval auth_ip_marker=if(event_id=4624,src_ip,null())
| streamstats current=f last(auth_time_marker) as auth_time last(auth_ip_marker) as auth_src_ip by user
```

This carried authentication time and source IP into later process events.

## Time Correlation

```spl
| eval time_since_auth=_time-auth_time
| where event_id=4688 AND time_since_auth <= 300
```

Lab timing:

```text
PowerShell → 60 seconds
CMD        → 120 seconds
```

## Suspicious PowerShell

Indicators:

```text
encodedcommand | -enc | executionpolicy | download | iex
```

```spl
| eval suspicious=if(match(lower(command),"encodedcommand|-enc|executionpolicy|download|iex"),1,0)
| where suspicious=1
```

## Parent Risk

```spl
| eval parent_risk=if(match(lower(parent),"winword.exe|excel.exe|outlook.exe"),1,0)
```

Controlled test:

```text
winword.exe → powershell.exe
parent_risk = 1
```

## Risk Scoring

```spl
| eval risk_score=(suspicious*2)+(parent_risk*3)
```

```spl
| eval severity=case(risk_score>=5,"High",risk_score>=2,"Medium",true(),"Low")
```

Positive test:

```text
suspicious=1
parent_risk=1
risk_score=5
severity=High
```

## Detection Output

```spl
| eval detection="Suspicious PowerShell After Authentication"
| table _time detection severity user auth_src_ip time_since_auth parent process pid command
```

## Positive Validation

```text
Administrator | 10.49.108.48
winword.exe → powershell.exe
powershell.exe -EncodedCommand ABC123
Authentication → 60 seconds earlier
```

Result:

```text
Suspicious PowerShell After Authentication
Severity: High
```

**PASS**

## Negative Validation

```text
explorer.exe → powershell.exe
powershell.exe -NoProfile
```

Result:

```text
suspicious=0
No detection
```

Suspicious PowerShell without recent authentication also failed the five-minute condition.

**PASS**

## Source-IP Finding

The `4688` event lacked a useful `src_ip`. The `4624` event provided `10.49.108.37`, which correlation exposed as:

```text
auth_src_ip=10.49.108.37
```

## Key Lessons

PowerShell alone should not automatically alert. Multiple signals, `streamstats`, time windows, and parent-process context provide stronger detection logic. Positive and negative tests are required.

## Limitations

This is a lab prototype. Production use requires tuning, boundary testing, broader telemetry, baselining, and additional validation.

## Outcome

```text
Raw Events → Correlation → Detection → Risk → Validation
```

Normal PowerShell did not alert; the controlled encoded-PowerShell test generated a High-severity detection.

**Status: Lab validated.**
