# Investigation Report

## Project
Windows Authentication Log Investigation: Failed Logons & Privilege Events (Splunk SPL)

## 1. Objective
Investigate Windows authentication failures, identify repeated failed-logon activity, and correlate successful logons with special privilege assignments using Splunk.

## 2. Data and Environment
Splunk Enterprise with Windows Security Event Logs provided in the SIEM Xpert training lab. Figures are from searches run on 16 Nov 2026.

## 3. Investigation

- Counted events by Event ID.
- Compared failed and successful logons per target account.
- Charted failed logons per hour to find spikes.
- Grouped failures into five-minute windows (5 or more per account and host).
- Inspected the raw events of the largest burst.
- Counted privilege assignments (4672) by account and host.
- Correlated a 4624 logon with its 4672 event using the Logon ID.

## 4. Findings

- 2,074 failed logons (4625), 282,773 successful logons (4624) and 62,981 special privilege assignments (4672).
- 41 five-minute windows contained 5 or more failures. The largest was 268 failures between 22:20 and 22:25 on 4 Nov 2026 against one username, on `SearchHead1` (Logon Type 3 in the events inspected), reason "Unknown user name or bad password".
- None of the failing usernames shown had a successful logon in the indexed data.
- No 4728 or 4732 events (no accounts added to privileged groups).
- `Arcsight3` accounted for almost all 4672 events. A Type 3 network logon for this account (Logon ID `0x1D735272B4`) matched a 4672 event listing administrative privileges.
- The source network address was not populated in the failed-logon events.

## 5. Assessment

- The failed-logon bursts are consistent with automated password guessing (T1110), but there is no evidence of a successful compromise and the source could not be determined.
- The privileged logon appears to be routine service or administrative activity (T1078 considered only as a possible interpretation). This is preliminary and is not treated as benign until the account owner and expected activity are validated.
- The available lab evidence does not confirm a brute-force attack or malicious privilege escalation.

## 6. Recommended Follow-up

- Confirm what `Arcsight3` is used for and whether its privileges are required.
- Capture the source address for failed logons so activity can be attributed.
- Create a saved alert for repeated failures and allowlist known service accounts.
- Monitor repeated failures that are followed by a successful logon for the same account.
- Escalate when activity is supported by evidence.

## 7. Disclaimer
This is an educational lab investigation, not a confirmed real-world security incident.
