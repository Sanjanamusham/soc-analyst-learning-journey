# Incident 01 — Windows Failed Logon Investigation

## 1. Incident Overview

| Field | Details |
|---|---|
| Incident Name | Windows Authentication Failure Investigation |
| Incident Type | Failed Authentication Activity |
| Severity | Low / Inconclusive (lab assessment) |
| Status | Evidence reviewed; verdict documented |
| SIEM | Splunk Enterprise |
| Endpoint | Windows Server 2022 |
| Event ID | 4625 |
| Index | wineventlog |
| Sourcetype | WinEventLog:Security |
| Environment | Isolated VMware Workstation Lab |

## 2. Objective

Investigate Windows Security Event ID 4625, identify failed logon activity, examine the target account, source address, logon type, and failure reason, and determine whether the evidence supports a brute-force conclusion.

## 3. Data Collection Validation

Splunk log collection was verified using:

```spl
index=*
| stats count by index, sourcetype, host
```

Observed sources during the validation search:

| Index | Sourcetype | Host | Events |
|---|---|---|---:|
| main | syslog | kali | 5,462 |
| wineventlog | WinEventLog:Application | WIN-TU878J0IPCG | 128 |
| wineventlog | WinEventLog:Security | WIN-TU878J0IPCG | 482 |
| wineventlog | WinEventLog:System | WIN-TU878J0IPCG | 673 |

These results confirm that Splunk was receiving Kali syslog and Windows Application, Security, and System events during the selected time range.

## 4. Event Description

Windows Security Event ID 4625 records a failed logon. A failure may result from incorrect credentials, account issues, application/service configuration, or malicious password guessing. A 4625 event alone does not establish an attack.

## 5. Verified Findings

The raw search returned **8 Event ID 4625 records** in the selected Last 24 Hours range.

| Finding | Verified observation |
|---|---|
| Affected host | WIN-TU878J0IPCG |
| Failed target accounts | soctest (5 events); DELL (3 events) |
| Source addresses | ::1 and 127.0.0.1 |
| Source interpretation | IPv6 and IPv4 loopback; local host |
| Logon types | 2 (Interactive); 7 (Unlock) |
| Failure reason | Unknown user name or bad password |
| Status | 0xC000006D |
| Sub-status | 0xC000006A (incorrect password) |
| Caller process | C:\\Windows\\System32\\svchost.exe |
| External source IP identified | No |

### Important field-extraction note

The Splunk-extracted `Account_Name` and `Account_Domain` fields contain multiple values in these 4625 records: the Subject account and the account for which the logon failed. Queries that group directly on these multivalue fields can inflate or duplicate statistics.

For this investigation, the raw Event ID 4625 messages were reviewed. The failed target account was the second value in the extracted `Account_Name` field for the events observed. Use `mvindex(Account_Name,1)` as the failed target account only after validating this extraction order against the raw event.

The raw-event count (8) is the verified total. Statistics that summed to more than 8 were not treated as unique-event counts.

## 6. Analysis

The events were generated on the local Windows host. Both `127.0.0.1` and `::1` are loopback addresses, not external attacker addresses. The observed logon types were interactive (2) and unlock (7). The failure sub-status `0xC000006A` indicates an incorrect password.

The events are consistent with local authentication failures, such as incorrect credentials or local authentication activity. The caller process `svchost.exe` is a legitimate Windows process name, but the process name alone does not identify the specific service responsible.

The available evidence does not establish a remote brute-force attack. The underlying cause of the local failures remains unconfirmed.

## 7. Analyst Verdict

**Verdict: Inconclusive — Local Failed Authentication Activity Observed**

Eight failed-logon events were identified in the selected 24-hour search. The failed target accounts were `soctest` (5 events) and `DELL` (3 events). The source addresses were loopback addresses and the events reported an incorrect-password sub-status.

No external source IP or confirmed malicious activity was identified in the reviewed evidence. The activity should not be labelled a confirmed brute-force attack.

## 8. Recommended Follow-up

- Verify whether the failed logons were expected in the lab.
- Review nearby successful logon events (Event ID 4624).
- Check whether any account lockout events (Event ID 4740) occurred.
- If further investigation is required, correlate the timestamps with relevant Windows service or application activity.
- Escalate only if additional evidence indicates unauthorized activity.

## 9. Lessons Learned

- Event ID 4625 is useful for investigating failed authentication.
- Raw event messages help validate extracted fields.
- Multivalue fields can inflate Splunk statistics if grouped without normalization.
- Loopback addresses indicate local activity, not a remote source.
- A detection is an investigation lead; it is not a final incident verdict.

## 10. Evidence

Evidence reviewed in Splunk:
- Data source inventory search.
- Event ID 4625 search.
- Raw failed-logon event details.
- Statistics by failed target account.

Screenshots should be added to the lab screenshots directory if they are retained as portfolio evidence.

## 11. Lab Safety

This investigation was performed in authorized virtual machines in an isolated VMware Workstation lab. No production systems or unauthorized accounts were targeted.
