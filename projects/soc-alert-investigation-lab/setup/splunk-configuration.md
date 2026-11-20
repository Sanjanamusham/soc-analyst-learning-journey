\# Splunk Enterprise Configuration



\## 1. Overview



This document describes the Splunk Enterprise configuration used in the SOC Alert Investigation and Incident Response Lab.



Splunk Enterprise is used as the centralized Security Information and Event Management (SIEM) platform to collect, search, monitor, and investigate security logs from Windows and Linux virtual machines.



\## 2. Splunk Environment



| Component | Details |

|---|---|

| SIEM Platform | Splunk Enterprise |

| Version | 10.0.1 |

| SIEM Operating System | Kali Linux |

| Log Sources | Windows Server 2022 and Linux |

| Log Collection | Splunk Universal Forwarder |

| Search Language | Splunk SPL |



\## 3. Data Collection



Security logs are collected from monitored endpoints using Splunk Universal Forwarders.



The forwarders transmit configured log data to Splunk Enterprise for indexing and analysis.



The collected data is used to investigate authentication activity, suspicious behavior, and system events.



\## 4. Data Sources



\### Windows Security Logs



Windows Security logs are collected from the Windows Server 2022 virtual machine.



Important events investigated include:



| Event ID | Description |

|---|---|

| 4624 | Successful logon |

| 4625 | Failed logon |

| 4648 | Logon using explicit credentials |



These events help identify authentication failures, successful logons, and suspicious authentication patterns.



\### Linux Logs



Linux logs are monitored to investigate authentication activity and system events.



Linux log data is used to practice reviewing authentication-related activity and identifying suspicious login patterns.



\## 5. Splunk Indexes



The Windows authentication investigation uses the following index:



| Index | Purpose |

|---|---|

| wineventlog | Windows Security event investigation |



The index and sourcetype are used to filter Windows Security events during investigations.



\## 6. Search and Investigation



Splunk Search \& Reporting is used to:



\- Search collected events.

\- Filter events by Event ID.

\- Review authentication activity.

\- Count failed logons.

\- Group events by host and account.

\- Identify suspicious authentication patterns.

\- Investigate successful and failed logons.

\- Review Linux authentication activity.



\## 7. Detection Searches



Detection searches are developed using Splunk Search Processing Language (SPL).



The Windows failed-logon detection identifies repeated Event ID 4625 events.



The detection search uses event counts grouped by host, account, and source network address.



\## 8. Dashboards



Dashboards are used to monitor:



\- Windows failed logons.

\- Windows successful logons.

\- Authentication failure trends.

\- Linux log source activity.

\- Monitored hosts.

\- Security event activity.



Dashboard screenshots are maintained in the dashboards/screenshots directory.



\## 9. Alert Configuration



A scheduled alert was configured for Windows multiple failed logons.



The alert uses a threshold-based detection search to identify three or more failed authentication events.



Alert configuration and detection search results are documented in the alerts directory and screenshots.



\## 10. Investigation Workflow



1\. Select the appropriate index and time range.

2\. Search for relevant security events.

3\. Filter events using Event IDs or relevant fields.

4\. Review event details.

5\. Group and count events to identify patterns.

6\. Correlate related authentication events.

7\. Determine the investigation verdict.

8\. Document findings and recommendations.



\## 11. Lab Safety



All Splunk configuration and investigations are performed in an isolated VMware Workstation lab.



The environment uses authorized virtual machines and controlled security event simulations.

