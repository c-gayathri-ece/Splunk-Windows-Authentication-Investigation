# Windows Failed Logon Investigation Using Splunk

## Project Objective
Investigate Windows failed-logon events using Splunk to understand authentication failures, event patterns, and their distribution over time.

## Tools and Technologies
- Splunk Enterprise
- Windows Security event logs
- Search Processing Language (SPL)
- Event ID 4625 — failed logon

## Investigation Process
1. Searched for Event ID 4625 in the `main` index.
2. Counted matching events within the selected seven-day time range.
3. Grouped events by status, substatus, and logon type.
4. Reviewed the hourly distribution using a timechart.
5. Inspected a sample event to review available fields.

## Key Findings
- The search returned 316 matching events in the selected seven-day window.
- One hourly time bucket contained 310 events.
- The inspected results included status and logon-type fields.
- A source IP address was not available in the fields inspected.

## Interpretation
The concentration of events in one hourly bucket may indicate a period of elevated authentication failures. Additional investigation is needed to understand the cause. The observed pattern alone does not confirm an attack.

## Limitations
- Findings apply only to the selected training-lab dataset and time range.
- Some events had missing extracted field values.
- The source IP address was not available in the inspected fields.
- No malicious activity was independently confirmed.

## Further Investigation
- Review raw events around the hourly spike.
- Identify affected accounts where the relevant fields are available.
- Investigate source host or IP information if available.
- Compare the activity with other relevant authentication and security logs.

## Conclusion
This exercise demonstrates basic Splunk searching, event counting, field-based grouping, timeline analysis, and cautious interpretation of Windows failed-logon events.

## Disclaimer
This is a training-lab project for educational purposes. The findings do not confirm a real security incident.
