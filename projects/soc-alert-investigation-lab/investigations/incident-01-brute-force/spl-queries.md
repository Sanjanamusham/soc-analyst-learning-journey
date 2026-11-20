# Incident 01 — Windows Failed Logon SPL Queries

Use the **Last 24 Hours** time range for the initial evidence searches.

## 1. Validate data sources

```spl
index=*
| stats count by index sourcetype host
```

## 2. Find failed Windows logons

```spl
index=wineventlog sourcetype="WinEventLog:Security" EventCode=4625
```

## 3. Count raw failed-logon events

```spl
index=wineventlog sourcetype="WinEventLog:Security" EventCode=4625
| stats count
```

## 4. Extract the failed target account

In the observed Event ID 4625 records, Splunk extracted both the Subject account and the failed target account into multivalue fields. Validate this order with a raw event before using the second value.

```spl
index=wineventlog sourcetype="WinEventLog:Security" EventCode=4625
| eval Failed_Account=mvindex(Account_Name,1)
| eval Failed_Account_Domain=mvindex(Account_Domain,1)
| stats count by Failed_Account Failed_Account_Domain
| sort - count
```

## 5. Review raw event details

```spl
index=wineventlog sourcetype="WinEventLog:Security" EventCode=4625
| eval Failed_Account=mvindex(Account_Name,1)
| eval Failed_Account_Domain=mvindex(Account_Domain,1)
| table _time RecordNumber host Failed_Account Failed_Account_Domain Source_Network_Address Workstation_Name Logon_Type Failure_Reason Status Sub_Status Caller_Process_Name Message
| sort - _time
```

## 6. Investigate failed logons by source and logon type

```spl
index=wineventlog sourcetype="WinEventLog:Security" EventCode=4625
| eval Failed_Account=mvindex(Account_Name,1)
| eval Failed_Account_Domain=mvindex(Account_Domain,1)
| stats count by host Failed_Account Failed_Account_Domain Source_Network_Address Logon_Type Failure_Reason Status Sub_Status
| sort - count
```

## 7. Five-minute threshold search (validated extraction)

```spl
index=wineventlog sourcetype="WinEventLog:Security" EventCode=4625
| eval Failed_Account=mvindex(Account_Name,1)
| bin _time span=5m
| stats count by _time host Failed_Account Source_Network_Address
| where count >= 3
| sort - count
```

**Note:** The multivalue extraction order must be checked against raw events. The searches above reflect the observed Event ID 4625 format in this lab. If field extraction changes, inspect the raw event and adjust the account extraction rather than relying on the field order.
