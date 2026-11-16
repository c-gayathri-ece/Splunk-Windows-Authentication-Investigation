# Splunk SPL Queries

Queries used in the investigation. Results are from the training-lab dataset, run with **All time** on 16 Nov 2026.

> **Field-mapping note:** In the events inspected for this training dataset, `Account_Name` contains multiple values and the target account appears as the last value. The queries therefore use `mvindex(Account_Name,-1)`. Windows event field extractions can differ by source and configuration; verify the raw event before applying this assumption to another dataset.

## 1. Event counts by Event ID

```spl
index=main (EventCode=4625 OR EventCode=4624 OR EventCode=4672 OR EventCode=4728 OR EventCode=4732)
| stats count by EventCode
| sort - count
```

Result: 4624 = 282,773; 4672 = 62,981; 4625 = 2,074; no 4728 or 4732 events.

## 2. Failed vs successful logons by target account

```spl
index=main (EventCode=4625 OR EventCode=4624)
| eval account=mvindex(Account_Name,-1)
| stats count(eval(EventCode=4625)) as failed_logons count(eval(EventCode=4624)) as successful_logons by account
| where failed_logons>=5
| sort - failed_logons
```

Purpose: find accounts with repeated failures and check whether any also logged on successfully.

## 3. Failed logons per hour

```spl
index=main EventCode=4625
| timechart span=1h count as failed_logins
```

Purpose: spot spikes. View as a column chart.

## 4. Repeated failed logons in five-minute windows

```spl
index=main EventCode=4625
| eval target_account=mvindex(Account_Name,-1)
| bin _time span=5m
| stats count as failed_attempts by _time target_account host
| where failed_attempts>=5
| sort - failed_attempts
```

Result: 41 windows; the largest was 268 failures (4 Nov 2026, 22:20).
The threshold of 5 is a starting value and should be tuned per environment.

## 5. Inspect the largest burst

```spl
index=main EventCode=4625
| where _time>=strptime("2026-11-04 22:20:00","%Y-%m-%d %H:%M:%S") AND _time<strptime("2026-11-04 22:25:00","%Y-%m-%d %H:%M:%S")
| table _time host Account_Name TargetUserName user IpAddress Source_Network_Address Logon_Type Failure_Reason Message
| head 30
```

Result: 268 events; Logon Type 3 in the rows displayed; failure reason "Unknown user name or bad password". Source address fields were empty.

## 6. Special privilege assignments by account and host

```spl
index=main EventCode=4672
| stats count by Account_Name host
| sort - count
```

## 7. Correlate a logon with its privilege assignment

```spl
index=main host=SearchHead1 (EventCode=4624 OR EventCode=4672) "0x1D735272B4"
| table _time EventCode Account_Name TargetUserName SubjectUserName SubjectLogonId TargetLogonId Logon_ID Logon_Type LogonType PrivilegeList Message
| sort _time
```

This is the exact example used in the investigation. It returned 9 matching events, including the 4624 logon and its 4672 privilege assignment. For another investigation, replace the Logon ID string with the value from the session being reviewed.

## Note

Field availability varies with the log source and field extractions, so check a raw event before relying on a field.
