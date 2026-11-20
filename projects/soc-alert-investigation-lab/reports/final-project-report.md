\# SOC Alert Investigation \& Incident Response Lab

\## Final Project Report



\*\*Project Type:\*\* Hands-on SOC Analyst L1 Lab  

\*\*SIEM Platform:\*\* Splunk Enterprise 10.0.1  

\*\*Virtualization Platform:\*\* VMware Workstation  

\*\*Operating Systems:\*\* Kali Linux and Windows Server 2022  

\*\*Log Collection:\*\* Splunk Universal Forwarder  

\*\*Investigation Language:\*\* Splunk SPL  

\*\*Environment:\*\* Isolated Virtual Lab  



\---



\## 1. Executive Summary



This project involved building a hands-on Security Operations Center (SOC) monitoring and investigation environment using VMware Workstation and Splunk Enterprise.



The environment was designed to collect security-related logs from Windows and Linux virtual machines using Splunk Universal Forwarders.



The collected telemetry was analyzed using Splunk Search Processing Language (SPL) to investigate authentication-related activity, identify suspicious patterns, review endpoint events, and practice basic incident response.



The project included log ingestion validation, authentication investigations, PowerShell activity analysis, Linux authentication log analysis, dashboard development, detection search validation, and alert configuration.



The objective was to gain practical experience with the responsibilities of an entry-level SOC Analyst, including security monitoring, alert triage, log analysis, event correlation, investigation, and documentation.



\---



\## 2. Project Objectives



The main objectives were:



\- Build a multi-source SIEM monitoring environment.

\- Configure Splunk Enterprise for security monitoring.

\- Collect Windows and Linux endpoint logs.

\- Investigate failed authentication attempts.

\- Correlate failed and successful authentication events.

\- Investigate suspicious PowerShell activity.

\- Analyze Linux authentication logs.

\- Develop SPL searches for security investigations.

\- Create monitoring dashboards.

\- Configure a scheduled security alert.

\- Document evidence, investigation findings, and recommendations.



\---



\## 3. Lab Environment



| Component | Configuration |

|---|---|

| Virtualization | VMware Workstation |

| SIEM | Splunk Enterprise 10.0.1 |

| SIEM Server | Kali Linux |

| Windows Endpoint | Windows Server 2022 |

| Linux Endpoint | Kali Linux |

| Log Collection | Splunk Universal Forwarder |

| Windows Log Source | Windows Security Event Log |

| Linux Log Source | Linux authentication and system logs |

| Investigation Language | Splunk SPL |

| Environment | Isolated VMware virtual machines |



\---



\## 4. Lab Architecture



The lab was configured with a Splunk Enterprise server running on Kali Linux and Windows and Linux endpoints forwarding logs to the SIEM.



The architecture included:



1\. Windows Server 2022 generating Windows Security events.

2\. Linux systems generating authentication and system logs.

3\. Splunk Universal Forwarders collecting endpoint telemetry.

4\. Splunk Enterprise receiving and indexing the logs.

5\. SPL searches used to analyze the collected data.

6\. Dashboards and alerts used for monitoring and detection.



\### Data Flow



Endpoint Systems → Splunk Universal Forwarder → Splunk Enterprise → Indexing → SPL Investigation → Dashboards and Alerts



\---



\## 5. Log Collection and SIEM Validation



The SIEM environment was configured and validated.



The following activities were completed:



\- Splunk Enterprise installation and startup verification.

\- Splunk receiving-port verification.

\- Splunk Universal Forwarder service verification.

\- Forwarding configuration validation.

\- Windows log ingestion verification.

\- Linux log ingestion verification.

\- Splunk index and sourcetype validation.

\- Host activity and data-source inventory searches.



Windows and Linux telemetry was visible in Splunk, confirming that the configured log sources were providing data to the monitoring environment.



\---



\## 6. Incident Investigations



\### Incident 01 – Windows Authentication Failure Investigation



\*\*Incident Type:\*\* Suspicious Authentication Activity



\*\*Severity:\*\* Medium – Lab Assessment



\*\*Event ID:\*\* 4625



\*\*Log Source:\*\* Windows Security Log



\*\*Verdict:\*\* Inconclusive – Suspicious Authentication Activity Observed



\#### Objective



Investigate repeated failed Windows logon attempts and determine whether the observed activity represented suspicious authentication behavior.



\#### Investigation



Windows Security Event ID 4625 was used to identify failed authentication attempts.



The investigation involved:



\- Searching for Event ID 4625.

\- Reviewing raw Windows Security events.

\- Identifying affected hosts and accounts.

\- Analyzing source network addresses.

\- Reviewing logon types.

\- Identifying authentication failure reasons.

\- Counting failed authentication events.

\- Applying threshold-based detection logic.

\- Reviewing related successful logon events.



\#### Observations



The investigation identified multiple failed authentication events.



The observed details included:



\- Event ID 4625.

\- Failure reason: Unknown user name or bad password.

\- Logon types included Type 2 (Interactive) and Type 7 (Unlock).

\- Source addresses included localhost addresses such as `127.0.0.1` and `::1`.

\- Multiple account and source-address combinations met the failed-authentication threshold in the detection search.



The local source addresses indicated that the observed authentication activity was associated with the endpoint itself rather than a confirmed external IP address.



\#### Detection Logic



The initial threshold investigation used a five-minute time-bucket approach to identify three or more failed authentication events.



A separate alert search was configured to review Event ID 4625 events within the previous 60 minutes and identify account and source-address combinations meeting the threshold.



\#### Analyst Verdict



\*\*Inconclusive – Suspicious Authentication Activity Observed\*\*



The repeated failed authentication attempts warranted investigation.



However, the available evidence did not conclusively establish a brute-force attack.



The activity could have been associated with incorrect credentials, local user activity, or another authentication process.



Further investigation would be required to determine whether the activity was malicious.



\#### Recommended Response



\- Verify the activity with the account owner.

\- Review the affected endpoint.

\- Check for successful logons after the failures.

\- Review related authentication events.

\- Investigate Event IDs 4624 and 4648.

\- Escalate suspicious activity if additional evidence is identified.



\---



\### Incident 02 – Authentication Anomaly Investigation



\*\*Objective:\*\* Correlate failed and successful logon events to investigate suspicious authentication activity.



The investigation involved reviewing authentication-related Windows events and examining the sequence of failed and successful logons.



The purpose was to identify authentication patterns that could require further investigation.



\#### Investigation Activities



\- Review failed authentication events.

\- Review successful authentication events.

\- Compare event timestamps.

\- Examine account names and source addresses.

\- Identify potentially suspicious authentication sequences.

\- Practice event correlation and alert triage.



\#### Skills Practiced



\- Windows authentication monitoring.

\- Event correlation.

\- Log analysis.

\- Account activity investigation.

\- Basic SOC alert triage.



\---



\### Incident 03 – Suspicious PowerShell Activity Investigation



\*\*Objective:\*\* Investigate controlled PowerShell execution and identify relevant endpoint telemetry.



The investigation involved examining PowerShell activity generated in the lab and reviewing relevant Windows logs to understand command execution behavior.



\#### Investigation Activities



\- Review PowerShell-related activity.

\- Identify relevant endpoint events.

\- Examine command execution telemetry.

\- Investigate suspicious execution patterns.

\- Document investigation evidence.



\#### Skills Practiced



\- Windows endpoint investigation.

\- PowerShell activity analysis.

\- Security event log review.

\- Suspicious command execution analysis.

\- Investigation documentation.



\---



\### Incident 04 – Linux Authentication Investigation



\*\*Objective:\*\* Analyze Linux authentication logs and investigate suspicious login activity.



The investigation involved examining Linux authentication telemetry and identifying relevant login-related events.



\#### Investigation Activities



\- Review Linux authentication logs.

\- Identify login-related events.

\- Investigate failed authentication activity.

\- Examine authentication-related log entries.

\- Practice Linux log analysis.



\#### Skills Practiced



\- Linux authentication log analysis.

\- SSH authentication investigation.

\- Failed login identification.

\- Linux endpoint monitoring.

\- Basic incident investigation.



\---



\## 7. Splunk Dashboards



Dashboards were created to provide visibility into the collected security telemetry and endpoint activity.



The dashboards included:



\- Windows Failed Logons Dashboard

\- Windows Successful Logons Dashboard

\- Windows Authentication Failure Trend

\- Linux Log Source Activity

\- Monitored Hosts Overview

\- Splunk Data Source Inventory



These dashboards supported monitoring and investigation by presenting endpoint activity and authentication-related information in a visual format.



\---



\## 8. Detection and Alert Configuration



\### Alert 01 – Windows Multiple Failed Logons



\*\*Alert Name:\*\* Windows Multiple Failed Logons



\*\*Alert Type:\*\* Scheduled



\*\*Schedule:\*\* Hourly, at 15 minutes past the hour



\*\*Detection Event:\*\* Windows Security Event ID 4625



\*\*Threshold:\*\* 3 or more failed logons



\*\*Search Window:\*\* Last 60 minutes



\*\*Severity:\*\* Medium



\*\*Trigger Action:\*\* Add to Triggered Alerts



\*\*Configuration Status:\*\* Saved and Enabled



\#### Detection Query



```spl

index=wineventlog EventCode=4625 earliest=-60m latest=now

| stats count by host Account\_Name Source\_Network\_Address

| where count >= 3

```



\#### Detection Validation



The detection query was manually executed in Splunk.



The search returned multiple results with failed-authentication counts meeting the configured threshold.



The alert was saved and enabled with the scheduled execution configuration.



The scheduled firing of the alert has not yet been independently verified.



The manually executed search confirms that the detection logic returned qualifying results, but it does not confirm that the scheduled alert successfully fired.



\#### Alert Evidence



\- `07-windows-failed-logon-alert-configuration.png`

\- `08-windows-failed-logon-detection-results.png`



\---



\## 9. Evidence Collection



Screenshots were captured to document the lab configuration, log collection, investigations, dashboards, and alert setup.



Evidence includes:



\- Splunk data inventory.

\- Windows failed logon events.

\- Windows successful logon events.

\- Windows authentication failure trends.

\- Linux log source activity.

\- Monitored hosts overview.

\- Windows Security Event ID 4625 investigation.

\- Alert configuration.

\- Detection search results.



The evidence is stored in the project's screenshots directory.



\---



\## 10. Incident Response Recommendations



Based on the investigations performed, the following general response actions were practiced:



\- Validate suspicious authentication activity.

\- Identify affected hosts and accounts.

\- Review authentication event timestamps.

\- Examine source addresses and logon types.

\- Correlate failed and successful authentication events.

\- Investigate suspicious endpoint activity.

\- Review relevant Windows and Linux logs.

\- Escalate suspicious findings to Tier 2 when required.

\- Document findings and maintain investigation evidence.



\---



\## 11. Skills Demonstrated



\### Security Monitoring



\- SIEM monitoring

\- Log ingestion validation

\- Endpoint monitoring

\- Security event analysis



\### SIEM and SPL



\- Splunk Enterprise

\- Splunk Search Processing Language

\- Event filtering

\- Statistics and aggregation

\- Threshold-based detection

\- Dashboard development

\- Alert configuration



\### Windows Security



\- Windows Security Event Logs

\- Event ID 4625

\- Event ID 4624

\- Authentication failure investigation

\- Successful logon investigation

\- PowerShell activity analysis



\### Linux Security



\- Linux authentication logs

\- SSH authentication investigation

\- Linux log analysis



\### SOC Operations



\- Alert triage

\- Event correlation

\- Investigation documentation

\- Incident verdict assessment

\- Basic incident response

\- Evidence collection



\### Technical Tools



\- VMware Workstation

\- Kali Linux

\- Windows Server 2022

\- Splunk Enterprise

\- Splunk Universal Forwarder

\- Git

\- GitHub



\---



\## 12. Project Safety



All activities were performed using authorized virtual machines in a controlled laboratory environment.



No real accounts, production systems, public targets, or destructive malware were used.



The project was designed for educational purposes and SOC Analyst L1 skill development.



\---



\## 13. Challenges and Learning Outcomes



During the project, practical challenges included configuring log forwarding, validating data ingestion, identifying relevant Windows and Linux log sources, writing SPL searches, analyzing authentication events, and configuring scheduled alerts.



These activities improved understanding of:



\- How a SIEM collects and centralizes logs.

\- How endpoint telemetry supports security investigations.

\- How Windows authentication events can be analyzed.

\- How Linux authentication logs can be investigated.

\- How SPL can be used to identify suspicious patterns.

\- How threshold-based detections can identify repeated activity.

\- Why alerts require investigation and contextual analysis.

\- Why evidence must be documented before assigning an incident verdict.



\---



\## 14. Conclusion



This project provided practical experience in building a SIEM monitoring environment using Splunk Enterprise, collecting endpoint logs from Windows and Linux systems, investigating authentication-related activity, analyzing PowerShell telemetry, creating dashboards, developing detection searches, and configuring scheduled alerts.



The lab demonstrates foundational SOC Analyst L1 capabilities in security monitoring, log analysis, alert triage, event correlation, investigation, and incident documentation.



The project also highlights the importance of investigating alerts using contextual evidence rather than classifying activity as malicious based only on detection thresholds.



The completed lab serves as a practical cybersecurity portfolio project demonstrating hands-on security operations experience in a controlled virtual environment.



