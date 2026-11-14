# Investigation Notes

## Windows Authentication Events

| Event ID | Description | Investigation purpose |
|---|---|---|
| 4625 | Failed logon | Identify authentication failures |
| 4624 | Successful logon | Review successful authentication |
| 4672 | Special privileges assigned to a new logon | Monitor privileged sessions |

## Detection Approach

- Review failed logons by account.
- Identify repeated failures within five-minute windows.
- Examine hourly authentication patterns.
- Inspect raw Windows security events.
- Correlate successful logons and special privilege assignments using Logon IDs.

## Important Investigation Notes

- A high number of failed logons does not automatically confirm a brute-force attack.
- Event ID 4672 does not automatically indicate malicious privilege escalation.
- Event correlation helps establish whether events belong to the same logon session.
- Findings must be validated against expected account and system behaviour.

## Investigation Outcome

Repeated failed-logon activity and a successful logon correlated with a special privilege assignment were observed in the training dataset. No confirmed malicious activity was established.
