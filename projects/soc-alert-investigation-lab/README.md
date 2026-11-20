# SOC Alert Investigation \& Incident Response Lab

## Project Overview

This project demonstrates a hands-on Security Operations Center (SOC) investigation environment built using VMware Workstation and Splunk Enterprise.

The lab simulates security events in isolated Windows and Linux virtual machines, collects endpoint logs using Splunk Universal Forwarders, and investigates suspicious activities using Splunk Search Processing Language (SPL).

The objective is to practice the responsibilities of a SOC Analyst L1, including alert triage, log analysis, event correlation, incident investigation, determining True Positive or False Positive verdicts, and documenting findings.

## Objectives

* Build a multi-source SIEM monitoring environment.
* Collect Windows and Linux security logs.
* Investigate authentication-related security events.
* Identify suspicious login patterns.
* Investigate suspicious PowerShell activity.
* Analyze Linux authentication logs.
* Develop Splunk searches for security investigations.
* Create security alerts and dashboards.
* Document investigation evidence and incident verdicts.
* Practice incident response recommendations.

## Lab Environment

|Component|Technology|
|-|-|
|Virtualization|VMware Workstation|
|SIEM|Splunk Enterprise|
|SIEM Server|Kali Linux|
|Windows Log Source|Windows Server 2022|
|Linux Log Source|Kali Linux|
|Log Collection|Splunk Universal Forwarder|
|Investigation Language|Splunk SPL|
|Environment|Isolated virtual lab|

## Lab Architecture

The lab consists of a Splunk server receiving security logs from Windows and Linux virtual machines.

The collected events are analyzed using Splunk searches, dashboards, and alerts.

## Investigations

### Incident 01 – Windows Brute-Force Detection

Investigate multiple failed Windows logon attempts and identify suspicious authentication patterns.

\# Incident 01 — Windows Brute-Force Detection



\## 1. Overview



\*\*Incident Name:\*\* Windows Authentication Failure Investigation



\*\*Incident Type:\*\* Suspicious Authentication / Brute-Force Detection



\*\*Severity:\*\* Medium (Lab Assessment)



\*\*Status:\*\* Investigated



\*\*Environment:\*\* Isolated VMware Workstation Lab



\## 2. Objective



Investigate Windows Security Event ID 4625, identify repeated authentication failures, and determine whether the activity represents suspicious authentication behavior.



\## 3. Lab Environment



| Component | Details |

|---|---|

| SIEM | Splunk Enterprise 10.0.1 |

| Endpoint | Windows Server 2022 |

| Log Source | Windows Security Log |

| Event ID | 4625 |

| Index | wineventlog |

| Sourcetype | WinEventLog:Security |

| Forwarder | Splunk Universal Forwarder |

| Environment | Isolated VMware Workstation |



\## 4. Alert Description



Windows Event ID 4625 records a failed logon attempt.



Repeated authentication failures against an account may indicate:



\- Brute-force attempts

\- Password guessing

\- Incorrect credentials

\- Misconfigured applications or services

\- Unauthorized authentication attempts



\## 5. Detection Logic



The investigation uses a threshold-based detection:



\- Event ID: 4625

\- Threshold: 3 or more failed logons

\- Time window: 5 minutes

\- Grouping: Host and account



\## 6. Investigation Queries



See `spl-queries.md` for the complete SPL queries used during the investigation.



\## 7. Investigation Findings



\*\*Affected Host:\*\* WIN-TU878J0IPCG



\*\*Target Account:\*\* WIN-TU878J0IPCGS / DELL



\*\*Failed Authentication Count:\*\* 4 events



\*\*Time Window:\*\* November 19, 2026, approximately 10:15:33 AM – 10:15:42 AM



\*\*Source IP:\*\* 127.0.0.1 (Localhost)



\*\*Logon Types Observed:\*\* 7 (Unlock) and 2 (Interactive)



\*\*Failure Reason:\*\* Unknown user name or bad password



\*\*Successful Logon Following Failures:\*\* Not confirmed



\### Findings Summary



Splunk returned four Windows Security Event ID 4625 events.



Three failed authentication events occurred within approximately nine seconds on November 19, 2026. These events were associated with the same endpoint and the source network address 127.0.0.1.



The observed logon types included Logon Type 7 (Unlock) and Logon Type 2 (Interactive).



The failure reason reported was "Unknown user name or bad password."



The repeated failures exceeded the configured detection threshold of three or More events within five minutes.



The source address 127.0.0.1 indicates that the authentication activity originated locally on the endpoint rather than from an external network IP address.



\## 8. Evidence



Screenshots are stored in the `screenshots` directory.



\- Windows Event Viewer Event ID 4625

\- Splunk raw authentication events

\- Failed authentication count

\- Threshold detection results

\- Investigation details

\- Splunk statistics showing account, source address, logon type, and failure reason



\## 9. Analyst Verdict



\*\*Verdict:\*\* Inconclusive — Suspicious Authentication Activity Observed



\*\*Reasoning:\*\*



The investigation identified multiple failed authentication attempts within a short period, exceeding the configured detection threshold.



However, the source IP address was 127.0.0.1, indicating local authentication activity. The observed logon types and failure reason could be associated with legitimate user activity, incorrect credentials, or suspicious behavior.



Based on the available evidence, the activity cannot be conclusively classified as a brute-force attack. Further investigation would be required to determine whether the activity was authorized or malicious.



\## 10. Recommended Response



Depending on the investigation findings:



\- Verify the activity with the account owner.

\- Review the source IP and workstation.

\- Check for successful authentication after failures.

\- Review additional authentication events.

\- Investigate related Event IDs such as 4624 and 4648.

\- Escalate suspicious activity to Tier 2.

\- Follow the organization's incident response procedure.



\## 11. Lessons Learned



\- Windows Event ID 4625 is useful for detecting authentication failures.

\- Splunk can centralize Windows Security logs.

\- Threshold-based detection can identify repeated failed logons.

\- Detection results require investigation before classifying an incident.

\- Context is necessary to distinguish suspicious activity from legitimate errors.

\- Source IP addresses and logon types provide valuable investigation context.



\## 12. Lab Safety



This activity was performed on Windows Server 2022 inside an isolated VMware Workstation lab using authorized test accounts and controlled authentication attempts.



\# Incident 01 — SPL Queries



\## 1. Search Failed Authentication Events



```spl

index=wineventlog sourcetype="WinEventLog:Security" EventCode=4625

```



\## 2. Display Failed Authentication Event Details



```spl

index=wineventlog sourcetype="WinEventLog:Security" EventCode=4625

| table \\\_time host Account\\\_Name TargetUserName Source\\\_Network\\\_Address IpAddress Logon\\\_Type Failure\\\_Reason

| sort - \\\_time

```



\## 3. Count Failed Logons by Host



```spl

index=wineventlog sourcetype="WinEventLog:Security" EventCode=4625

| stats count by host

```



\## 4. Count Failed Logons by Account



```spl

index=wineventlog sourcetype="WinEventLog:Security" EventCode=4625

| stats count by Account\\\_Name

| sort - count

```



\## 5. Threshold Detection — 3 Failures in 5 Minutes



```spl

index=wineventlog sourcetype="WinEventLog:Security" EventCode=4625

| bin \\\_time span=5m

| stats count by \\\_time, host, Account\\\_Name

| where count >= 3

| sort - count

```



\## 6. Review Failed and Successful Logons



```spl

index=wineventlog sourcetype="WinEventLog:Security" (EventCode=4625 OR EventCode=4624)

| table \\\_time host EventCode Account\\\_Name TargetUserName Source\\\_Network\\\_Address IpAddress Logon\\\_Type

| sort \\\_time

```



\## 7. Detection Explanation



The detection groups Windows failed authentication events into five-minute intervals.



Three or more failed authentication attempts against the same host and account during the interval trigger the detection.



This is a basic threshold detection and may generate false positives from legitimate users entering incorrect passwords.





### Incident 02 – Authentication Anomaly

Correlate failed and successful logon events to investigate suspicious authentication activity.

### Incident 03 – Suspicious PowerShell Activity

Investigate controlled PowerShell execution and identify relevant endpoint telemetry.

### Incident 04 – Linux Authentication Investigation

Analyze Linux authentication logs and investigate suspicious login activity.

## Skills Demonstrated

* SIEM monitoring
* Splunk Enterprise
* Log ingestion and analysis
* Windows Security Event Logs
* Linux authentication logs
* Splunk SPL
* Authentication investigation
* Event correlation
* Alert triage
* Incident documentation
* Basic incident response
* Git and GitHub documentation

## Safety

All security simulations are performed using authorized virtual machines in a controlled laboratory environment.

No real accounts, production systems, public targets, or destructive malware are used.

## Project Status

\- \[x] Splunk configuration verification

\- \[x] Windows log ingestion

\- \[x] Linux log ingestion

\- \[x] Incident 01 – Brute-force investigation

\- \[x] Incident 02 – Authentication anomaly

\- \[x] Incident 03 – PowerShell investigation

\- \[x] Incident 04 – Linux authentication investigation

\- \[x] Dashboard development

\- \[ ] Alert configuration

\- \[ ] Final incident report

\- \[x] VMware environment validation

\- \[x] Project screenshots

\- \[ ] GitHub documentation review

