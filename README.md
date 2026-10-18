# Windows Failed Logon Investigation Using Splunk

A beginner SOC analyst portfolio project investigating Windows failed-logon events using Splunk Search Processing Language (SPL).

## Project Overview

Windows Event ID **4625** records failed logon attempts. This project analyses matching events from a training-lab dataset to examine authentication-related fields, count events, and review their distribution over time.

## Objectives

- Search Windows failed-logon events.
- Count events within a selected time range.
- Group events by status, substatus, and logon type.
- Review hourly event patterns.
- Document findings, limitations, and recommended follow-up steps.

## Tools and Technologies

- Splunk Enterprise
- Search Processing Language (SPL)
- Windows Security event logs
- Windows Event ID 4625

## Investigation Workflow

1. Search for Event ID 4625 in the `main` index.
2. Count matching events.
3. Group events by authentication-related fields.
4. Visualise hourly event counts.
5. Inspect a sample event and document the findings.

## Key Findings

- **316** matching events were returned in the selected seven-day training-lab window.
- One hourly time bucket contained **310** events.
- A source IP address was not available in the fields inspected.

The concentration of events warrants further investigation but does not, by itself, confirm malicious activity.

## Project Structure

- [`queries/README.md`](queries/README.md) — SPL queries and their purposes.
- [`notes/README.md`](notes/README.md) — investigation notes and limitations.
- [`notes/investigation-report.md`](notes/investigation-report.md) — investigation report and recommended follow-up.
- `evidence/` — placeholder for approved, sanitised evidence if sharing is permitted.

## Skills Demonstrated

- Basic Splunk searching and filtering
- Event counting and statistical grouping
- Time-based event analysis
- Security-log interpretation
- Investigation documentation
- Evidence-based reporting and recognition of limitations

## Limitations

- Results depend on the selected training dataset and time range.
- Some events had missing extracted field values.
- Source IP information was not available in the fields inspected.
- No malicious activity was independently confirmed.

## Disclaimer

This project uses training-lab data for educational purposes. The findings should not be interpreted as confirmation of a real security incident. Training screenshots have not been published pending confirmation of sharing permission.
