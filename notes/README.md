# Investigation Notes

## Windows Authentication Events

| Event ID | Description | Investigation purpose |
|---|---|---|
| 4625 | Failed logon | Identify authentication failures |
| 4624 | Successful logon | Review successful authentication and logon type |
| 4672 | Special privileges assigned to a new logon | Monitor privileged sessions |
| 4728 / 4732 | Member added to a privileged group | Check for privilege changes (none found) |

## Detection Approach

- Count failed and successful logons per target account.
- Identify repeated failures within five-minute windows (5 or more per account and host).
- Review hourly failure patterns for spikes.
- Inspect raw events for logon type, failure reason and source address.
- Correlate successful logons and special privilege assignments using Logon IDs.

## Important Investigation Notes

- A high number of failed logons does not by itself confirm a brute-force attack.
- Event ID 4672 does not by itself indicate malicious privilege escalation.
- Correlating by Logon ID shows whether events belong to the same logon session.
- Findings must be validated against expected account and system behaviour.

## Investigation Outcome

- 2,074 failed logons; the largest burst was 268 failures in five minutes against a single username (host `SearchHead1`; Logon Type 3 in the events inspected).
- None of the failing usernames shown had a successful logon in the indexed data.
- The source network address was not populated, so the activity could not be attributed.
- `Arcsight3` accounts for almost all 4672 events; the correlated logon (Logon ID `0x1D735272B4`) was a Type 3 network logon with an administrative privilege set. This is a preliminary assessment of routine service or administrative activity; it is not treated as benign until the account owner and expected activity are validated.
- No confirmed malicious activity was established.
