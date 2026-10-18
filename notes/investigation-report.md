# Windows Failed Logon Investigation Report

## 1. Objective
Analyse Windows failed-logon events in Splunk and identify patterns that may require further investigation.

## 2. Data and Scope
- **Platform:** Splunk Enterprise
- **Index:** `main`
- **Event ID:** 4625 — failed logon
- **Time window:** Selected seven-day training-lab search window

## 3. Queries Performed
- Counted matching failed-logon events.
- Grouped events by status, substatus, and logon type.
- Visualised hourly event counts.
- Inspected a sample event.

See [`../queries/README.md`](../queries/README.md) for the SPL queries.

## 4. Findings
- **316** matching events were returned during the selected time window.
- One hourly time bucket contained **310** events.
- The inspected results included status, substatus, and logon-type fields.
- A source IP address was not available in the fields inspected.

## 5. Analysis
The concentration of events in one hourly bucket may indicate a period of elevated authentication failures. The available findings are insufficient to determine the cause or confirm malicious activity.

## 6. Recommended Follow-up
1. Review raw events within the high-volume hour.
2. Identify affected accounts where the required fields are available.
3. Check source host or IP information if available.
4. Correlate with other authentication and security logs.
5. Determine whether the activity is expected or suspicious before drawing conclusions.

## 7. Limitations
- Findings are specific to the selected training dataset and time window.
- Some events had missing extracted field values.
- Source IP information was not available in the inspected fields.
- No real security incident was independently confirmed.

## 8. Conclusion
This investigation demonstrates basic Splunk searching, event aggregation, timeline analysis, and cautious interpretation of authentication failures.

## Disclaimer
This is an educational training-lab project. The findings do not confirm a real security incident. No training-lab screenshots are included in this report.
