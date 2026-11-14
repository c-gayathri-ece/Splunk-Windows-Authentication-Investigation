# Splunk SPL Queries

These queries were used during the Windows security log investigation.

## 1. Count Failed Logons

```spl
index=main EventCode=4625
| stats count
```

## 2. Analyse Failed Logons by Account

```spl
index=main (EventCode=4625 OR EventCode=4624)
| eval account=coalesce(Account_Name, TargetUserName, user)
| stats count(eval(EventCode=4625)) as failed_logons count(eval(EventCode=4624)) as successful_logons by account
| where failed_logons>=5
| sort - failed_logons
```

## 3. Failed Logon Timeline

```spl
index=main EventCode=4625
| timechart span=1h count as failed_logins
```

## 4. Detect Repeated Failed Logons

```spl
index=main EventCode=4625
| bin _time span=5m
| stats count as failed_attempts by _time Account_Name host
| where failed_attempts>=5
| sort - failed_attempts
```

## 5. Analyse Special Privilege Assignments

```spl
index=main EventCode=4672
| stats count by Account_Name host
| sort - count
```

## 6. Investigate Logon and Privilege Events

```spl
index=main host=SearchHead1 (EventCode=4624 OR EventCode=4672) "<LOGON_ID>"
| table _time EventCode Account_Name SubjectUserName PrivilegeList Message
| sort _time
```

Replace `<LOGON_ID>` with the Logon ID from the lab event being investigated.

## Note

These queries were tested against a training-lab dataset. Field availability and results may vary depending on the Windows log source and Splunk field extractions.
