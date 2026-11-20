

\# Incident 03 — PowerShell Investigation SPL Queries



\## 1. Search PowerShell Operational Events



Search for PowerShell Operational log events.



```spl

index=wineventlog EventCode=4103 OR EventCode=4104

```



\## 2. Search Script Block Logging Events



Event ID 4104 can contain PowerShell script block content when script block logging is enabled.



```spl

index=wineventlog EventCode=4104

```



\## 3. Review PowerShell Event Details



Review timestamps, host, event ID, and available event details.



```spl

index=wineventlog EventCode=4104

| table \_time host EventCode Message

| sort - \_time

```



\## 4. Count PowerShell Events by Host



Identify the hosts generating PowerShell events.



```spl

index=wineventlog EventCode=4104

| stats count by host

| sort - count

```



\## 5. Count PowerShell Events by Event ID



Review the distribution of PowerShell event IDs.



```spl

index=wineventlog EventCode=4103 OR EventCode=4104

| stats count by EventCode

| sort - count

```



\## 6. Search for Suspicious PowerShell Keywords



Search for potentially suspicious keywords within available PowerShell event data.



```spl

index=wineventlog EventCode=4104

| search Message="\*EncodedCommand\*" OR Message="\*DownloadString\*" OR Message="\*Invoke-Expression\*" OR Message="\*FromBase64String\*"

| table \_time host EventCode Message

| sort - \_time

```



\## 7. Search for PowerShell Process Creation



Search Windows Security Event ID 4688 for process creation events involving PowerShell.



```spl

index=wineventlog EventCode=4688

| search New\_Process\_Name="\*powershell.exe\*" OR New\_Process\_Name="\*pwsh.exe\*" OR Process\_Name="\*powershell.exe\*"

| table \_time host Account\_Name New\_Process\_Name Process\_Name CommandLine

| sort - \_time

```



Field names may differ depending on the Windows event configuration and Splunk field extraction.



\## 8. Investigation Workflow



1\. Identify PowerShell events.

2\. Review event timestamps.

3\. Identify the host and executing account.

4\. Review script block contents.

5\. Identify suspicious commands or parameters.

6\. Review related process creation events.

7\. Correlate with other endpoint activity.

8\. Determine the investigation verdict.



\## 9. Investigation Considerations



PowerShell is a legitimate Windows administration tool.



The presence of PowerShell commands does not automatically indicate malicious activity.



Suspicious commands should be reviewed in context, including the executing user, host, command content, and surrounding events.



\## 10. Limitations



PowerShell logging depends on the logging configuration.



Event ID 4104 may not be available if script block logging is not enabled.



Field names and extracted command content may vary depending on the event collection configuration.



