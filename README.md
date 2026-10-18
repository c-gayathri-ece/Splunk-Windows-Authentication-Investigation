# Windows Failed Logon Investigation Using Splunk

A beginner SOC investigation project analysing Windows failed-logon events using Splunk Search Processing Language (SPL).

## Project Overview

This project explores Windows Security Event ID **4625**, which records failed logon attempts. The investigation uses Splunk searches and statistical commands to summarise authentication failures and review their distribution over time.

## Objectives

- Search for failed-logon events.
- Count matching events within a selected time range.
- Group events by status, substatus, and logon type.
- Review the hourly distribution of events.
- Document findings and investigation limitations.

## Tools and Technologies

- Splunk Enterprise
- Search Processing Language (SPL)
- Windows Security event logs

## Investigation Workflow

1. Search for Event ID 4625.
2. Calculate the total number of matching events.
3. Group events by available authentication-related fields.
4. Review the hourly event timeline.
5. Record findings without assuming that every failure is malicious.

## Key Finding

In the selected seven-day training-lab search window, 316 matching events were observed. One hourly bucket contained 310 events. This concentration warrants further investigation but does not, by itself, establish malicious activity.

## Limitations

- A source IP address was not available in the inspected fields.
- Some events had missing extracted field values.
- Findings are specific to the dataset and selected time range.
- The investigation did not independently confirm an attack.

## Project Structure

- `evidence/` — approved, sanitised investigation screenshots
- `queries/` — SPL queries and explanations
- `notes/` — investigation notes and lessons learned

## Skills Demonstrated

- Basic SPL searching and filtering
- Event counting and statistical grouping
- Sorting and timeline analysis
- Security-log interpretation
- Documentation of findings and limitations

## Disclaimer

This is a training-lab investigation created for learning purposes. Results describe the selected dataset and should not be interpreted as confirmation of a real security incident.
