# End-to-End Windows Brute-Force & Privilege Escalation Detection (Splunk SPL)

## Project Overview

A SOC Analyst L1 portfolio project using Splunk Enterprise and SPL to investigate Windows authentication failures, identify repeated failed-logon activity, and correlate successful logons with special privilege assignments.

The project uses Windows Security Event Logs from a training-lab dataset.

## Objectives

- Investigate Windows failed logon events (Event ID 4625).
- Analyse successful logons (Event ID 4624).
- Identify repeated failed-logon activity within short time windows.
- Monitor special privilege assignments (Event ID 4672).
- Correlate logon and privilege events using Logon IDs.
- Document findings, limitations, and recommended investigation steps.

## Tools and Technologies

- Splunk Enterprise
- Splunk Search Processing Language (SPL)
- Windows Security Event Logs
- Windows Event IDs 4625, 4624 and 4672

## Investigation Workflow

1. Search Windows failed-logon events using Event ID 4625.
2. Count and analyse failed and successful authentication events.
3. Group failed logons by account and review hourly activity.
4. Detect repeated failed attempts within five-minute windows.
5. Inspect raw failed-logon events for additional context.
6. Investigate Event ID 4672 for special privilege assignments.
7. Correlate Event IDs 4624 and 4672 using the same Logon ID.
8. Document findings and recommend further validation.

## Key Findings

- **2,121** Event ID 4625 events were returned in a selected lab-data search.
- Repeated failed-logon activity was identified using a five-minute detection window.
- One five-minute bucket contained a high volume of failed attempts and was selected for further inspection.
- Event ID 4672 records showed special privilege assignments.
- A successful network logon (Event ID 4624) was correlated with an Event ID 4672 using the same Logon ID.
- The correlated session involved the account `Arcsight3`, with source address `192.168.0.125` and Logon Type 3.

These findings demonstrate investigation and event correlation. They do not independently confirm a brute-force attack or malicious privilege escalation.

## Project Structure

- `queries/README.md` — SPL queries and their purposes.
- `notes/README.md` — Investigation notes and limitations.
- `notes/investigation-report.md` — Investigation report and recommendations.
- `evidence/` — Sanitised screenshots and approved lab evidence.

## Skills Demonstrated

- Splunk searching and filtering
- Windows authentication event analysis
- Failed-logon monitoring
- Time-based event analysis
- Repeated authentication failure detection
- Special privilege event monitoring
- Event correlation using Logon IDs
- Security investigation documentation
- Evidence-based reporting

## Limitations

- Results depend on the training dataset and selected time range.
- Some extracted fields were missing or inconsistently mapped.
- Repeated or high-volume events require validation against the original event records.
- Event ID 4672 alone does not indicate malicious privilege escalation.
- No confirmed security incident was established from the available evidence.

## Disclaimer

This project uses training-lab data for educational and portfolio purposes. Findings are not confirmation of a real-world security incident. Evidence should be sanitised before public sharing.
