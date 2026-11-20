

\# Incident 02 — Authentication Anomaly SPL Queries



\## 1. Search Authentication Events



Search for Windows successful logons, failed logons, and explicit credential usage.



```spl

index=wineventlog sourcetype="WinEventLog:Security" (EventCode=4624 OR EventCode=4625 OR EventCode=4648)

```



\## 2. Display Authentication Event Details



Review authentication events with relevant investigation fields.



```spl

index=wineventlog sourcetype="WinEventLog:Security" (EventCode=4624 OR EventCode=4625 OR EventCode=4648)

| table \_time host EventCode Account\_Name TargetUserName Source\_Network\_Address IpAddress Logon\_Type

| sort - \_time

```



\## 3. Count Authentication Events by Event ID



Determine the number of events for each authentication event ID.



```spl

index=wineventlog sourcetype="WinEventLog:Security" (EventCode=4624 OR EventCode=4625 OR EventCode=4648)

| stats count by EventCode

| sort - count

```



\## 4. Count Events by Account



Review authentication activity associated with each account.



```spl

index=wineventlog sourcetype="WinEventLog:Security" (EventCode=4624 OR EventCode=4625 OR EventCode=4648)

| stats count by Account\_Name

| sort - count

```



\## 5. Review Failed Logons



Search for failed authentication events.



```spl

index=wineventlog sourcetype="WinEventLog:Security" EventCode=4625

| table \_time host Account\_Name TargetUserName Source\_Network\_Address IpAddress Logon\_Type

| sort - \_time

```



\## 6. Review Successful Logons



Search for successful authentication events.



```spl

index=wineventlog sourcetype="WinEventLog:Security" EventCode=4624

| table \_time host Account\_Name TargetUserName Source\_Network\_Address IpAddress Logon\_Type

| sort - \_time

```



\## 7. Review Explicit Credential Usage



Search for Event ID 4648.



```spl

index=wineventlog sourcetype="WinEventLog:Security" EventCode=4648

| table \_time host Account\_Name TargetUserName Source\_Network\_Address IpAddress

| sort - \_time

```



\## 8. Authentication Timeline



Create a timeline of successful and failed logons.



```spl

index=wineventlog sourcetype="WinEventLog:Security" (EventCode=4624 OR EventCode=4625)

| sort \_time

| table \_time host EventCode Account\_Name TargetUserName Source\_Network\_Address Logon\_Type

```



\## 9. Count Authentication Events by Host



Identify hosts generating authentication activity.



```spl

index=wineventlog sourcetype="WinEventLog:Security" (EventCode=4624 OR EventCode=4625 OR EventCode=4648)

| stats count by host EventCode

| sort - count

```



\## 10. Investigation Explanation



These searches help the analyst review authentication activity and identify potentially unusual behavior.



The analyst should correlate successful and failed authentication events, review account names, source addresses, logon types, and timestamps.



\## 11. Limitations



The available fields may vary depending on Windows event configuration and the data collected by Splunk.



If a field is unavailable, inspect the raw event to identify the correct field name.



An authentication anomaly should not automatically be classified as malicious without supporting evidence.



