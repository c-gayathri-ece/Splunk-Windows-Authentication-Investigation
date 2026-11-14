# Investigation Report

## Project
End-to-End Windows Brute-Force & Privilege Escalation Detection (Splunk SPL)

## 1. Objective
Investigate Windows authentication failures, identify repeated failed-logon activity, and correlate successful logons with special privilege assignments using Splunk.

## 2. Investigation

- Searched Event ID 4625 to identify failed logons.
- Analysed failed and successful logon events.
- Used a five-minute time window to identify repeated failed attempts.
- Inspected raw events for additional context.
- Analysed Event ID 4672 for special privilege assignments.
- Correlated Event IDs 4624 and 4672 using the Logon ID.

## 3. Findings

- 2,121 failed-logon events (4625) were found in the selected search.
- Repeated failed-logon activity was identified and selected for investigation.
- Special privilege assignment events (4672) were observed.
- A successful network logon (4624) and special privilege assignment (4672) were correlated to the same logon session.
- The observed activity requires validation against expected account behaviour.

## 4. Conclusion

The investigation demonstrated how Splunk can be used to monitor failed authentication attempts, identify repeated activity, inspect privileged logons, and correlate Windows security events.

The available lab evidence does not independently confirm a brute-force attack or malicious privilege escalation.

## 5. Recommended Follow-up

- Validate whether the account activity was expected.
- Investigate source systems and authentication patterns.
- Review account privileges and access requirements.
- Monitor repeated authentication failures.
- Escalate suspicious activity for further investigation when supported by evidence.

## 6. Environment

Splunk Enterprise and Windows Security Event Logs from a training-lab dataset.

## 7. Disclaimer

This is an educational lab investigation, not a confirmed real-world security incident.
