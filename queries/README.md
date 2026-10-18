# Windows Failed Logon Investigation — SPL Queries

## 1. Count All Failed Logon Events

**Purpose:** Establish the total number of Event ID 4625 events in the selected time range.

```spl
index=main EventCode=4625
| stats count
```

## 2. Group Events by Authentication Fields

**Purpose:** Compare event counts by status, substatus, and logon type.

```spl
index=main EventCode=4625
| stats count by Status Sub_Status Logon_Type
| sort -count
```

## 3. View Failed Logons Over Time

**Purpose:** Visualise the hourly distribution and identify spikes that may need investigation.

```spl
index=main EventCode=4625
| timechart span=1h count
```

## 4. Inspect a Sample Event

**Purpose:** Display one matching event for an initial review of its available fields.

```spl
index=main EventCode=4625
| head 1
```

## Interpretation Note

Results depend on the selected time range and available training-lab data. A concentration of failed logons warrants further investigation but does not, by itself, confirm malicious activity.
