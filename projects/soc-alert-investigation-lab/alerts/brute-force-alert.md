# Windows Brute-Force Detection Alert

## 1. Overview

This detection identifies repeated Windows authentication failures that may warrant investigation. It uses Windows Security Event ID 4625 and is an investigation trigger—not confirmation of a brute-force attack.

## 2. Alert Details

| Field | Details |
|---|---|
| Alert Name | Windows Multiple Failed Logons |
| Detection Type | Authentication Monitoring |
| SIEM | Splunk Enterprise |
| Log Source | Windows Security Logs |
| Event ID | 4625 |
| Severity | Medium (investigation) |
| Detection Threshold | 3 or more failed logons |
| Time Window | 5 minutes |
| Status | SPL documented; scheduled firing requires validation |

## 3. Detection Objective

Identify repeated failed authentication attempts within a short period. Possible causes include password guessing, incorrect passwords, account lockout activity, and misconfigured applications or services.

## 4. Field Extraction Consideration

In the observed Windows 4625 events, Splunk extracted the Subject account and failed target account into multivalue `Account_Name` and `Account_Domain` fields. Grouping directly by `Account_Name` can produce misleading results.

The SPL below uses the second extracted account value as the failed target account, based on the raw events reviewed in this lab. Confirm this order against raw events if the event format or field extraction changes.

## 5. SPL Detection Query

```spl
index=wineventlog sourcetype="WinEventLog:Security" EventCode=4625
| eval Failed_Account=mvindex(Account_Name,1)
| bin _time span=5m
| stats count by _time host Failed_Account Source_Network_Address
| where count >= 3
| sort - count
```

## 6. Trigger Condition

- Windows Security Event ID 4625.
- Three or more failed logons in a five-minute bucket.
- Grouped by time bucket, host, failed target account, and source address.

When the threshold is met, review the account, source, logon type, failure reason, and nearby successful logons before assigning a verdict.

## 7. Analyst Investigation

1. Identify the affected host and failed target account.
2. Review the source IP address.
3. Examine timestamps and failure frequency.
4. Check logon type and failure status/sub-status.
5. Search for successful logons before or after the failures.
6. Review related events and endpoint context.
7. Determine whether the activity is expected, suspicious, or inconclusive.
8. Document evidence and escalate if warranted.

## 8. False Positive Considerations

Possible legitimate causes include incorrect password entry, forgotten passwords, password changes, account lockout activity, misconfigured applications, and services using outdated credentials.

## 9. Analyst Verdict

The detection is an investigation trigger. It does not automatically confirm brute-force activity. Validate the target account, host, source address, and surrounding telemetry.

## 10. Lab Environment

This detection is intended for authorized security monitoring and investigation in an isolated VMware Workstation lab.
