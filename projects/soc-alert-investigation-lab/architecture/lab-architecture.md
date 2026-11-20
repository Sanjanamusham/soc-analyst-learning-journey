\# SOC Lab Architecture



\## 1. Overview



This document describes the architecture of the SOC Alert Investigation and Incident Response Lab.



The lab is built using VMware Workstation and Splunk Enterprise to simulate a small Security Operations Center (SOC) monitoring environment.



The purpose of the lab is to collect security logs from Windows and Linux systems, centralize them in Splunk, and investigate suspicious activity using Search Processing Language (SPL).



\## 2. Lab Components



| Component | Technology |

|---|---|

| Virtualization Platform | VMware Workstation |

| SIEM Platform | Splunk Enterprise 10.0.1 |

| SIEM Server | Kali Linux |

| Windows Log Source | Windows Server 2022 |

| Linux Environment | Kali Linux |

| Log Collection | Splunk Universal Forwarder |

| Log Analysis | Splunk Search \& Reporting |

| Investigation Language | SPL |

| Environment | Isolated Virtual Machines |



\## 3. Architecture



The lab contains virtual machines operating within VMware Workstation.



The Splunk Enterprise server receives logs from monitored Windows and Linux systems through Splunk Universal Forwarders.



Collected logs are stored in Splunk indexes and analyzed using searches, statistics, dashboards, and alerts.



\### Log Flow



1\. Security events are generated on Windows and Linux endpoints.

2\. Splunk Universal Forwarders collect configured log sources.

3\. Forwarders transmit collected events to Splunk Enterprise.

4\. Splunk indexes and stores the incoming data.

5\. The analyst searches and analyzes events using SPL.

6\. Dashboards provide an overview of monitored systems and security activity.

7\. Detection searches identify suspicious activity.

8\. Alerts are configured to notify the analyst about qualifying events.



\## 4. Architecture Diagram



```text

&#x20;                VMware Workstation

&#x20;             Isolated Virtual Lab

&#x20;                      |

&#x20;       +--------------+--------------+

&#x20;       |                             |

&#x20;       |                             |

+----------------------+    +----------------------+

|   Kali Linux VM     |    | Windows Server 2022 |

|                      |    |                      |

| Splunk Enterprise    |    | Windows Security     |

| SIEM Server          |    | Event Logs           |

|                      |    |                      |

| Search \& Reporting   |    | Splunk Universal    |

| Dashboards           |    | Forwarder            |

| Alerts               |    |                      |

+----------+-----------+    +----------+-----------+

&#x20;          |                           |

&#x20;          |                           |

&#x20;          +-----------+---------------+

&#x20;                      |

&#x20;             Splunk Log Collection

&#x20;                      |

&#x20;             +----------------------+

&#x20;             | Splunk Indexes      |

&#x20;             |                      |

&#x20;             | wineventlog         |

&#x20;             | Linux Log Sources   |

&#x20;             +----------------------+

&#x20;                      |

&#x20;             +----------------------+

&#x20;             | SOC Analyst          |

&#x20;             |                      |

&#x20;             | SPL Investigations   |

&#x20;             | Dashboard Monitoring |

&#x20;             | Alert Triage         |

&#x20;             | Incident Reporting   |

&#x20;             +----------------------+

```



\## 5. Windows Log Collection



The Windows Server 2022 virtual machine is configured as a monitored endpoint.



Windows Security logs are collected and analyzed for authentication-related activity.



Important Windows Security Event IDs investigated in this lab include:



| Event ID | Description |

|---|---|

| 4624 | Successful logon |

| 4625 | Failed logon |

| 4648 | Logon using explicit credentials |



The collected Windows events are used to investigate authentication failures, successful logons, and suspicious authentication patterns.



\## 6. Linux Log Collection



Linux authentication logs are monitored to investigate login activity.



The Linux environment is used to practice identifying authentication-related events, reviewing log activity, and investigating suspicious login behavior.



The collected logs are analyzed using Splunk searches and dashboard panels.



\## 7. Splunk Data Flow



The general data flow is:



```text

Endpoint Logs

&#x20;    |

&#x20;    v

Splunk Universal Forwarder

&#x20;    |

&#x20;    v

Splunk Enterprise

&#x20;    |

&#x20;    v

Data Indexing

&#x20;    |

&#x20;    v

SPL Searches

&#x20;    |

&#x20;    +----> Dashboards

&#x20;    |

&#x20;    +----> Detection Searches

&#x20;    |

&#x20;    +----> Alerts

&#x20;    |

&#x20;    +----> Incident Investigations

```



\## 8. Security Monitoring Use Cases



The lab focuses on the following monitoring use cases:



\- Multiple failed Windows logon attempts.

\- Suspicious authentication activity.

\- Successful logons following authentication failures.

\- PowerShell activity investigation.

\- Linux authentication log investigation.

\- Monitoring log source activity.

\- Identifying suspicious patterns through event analysis.



\## 9. Analyst Workflow



The SOC Analyst L1 workflow practiced in this lab:



1\. Monitor dashboards and security events.

2\. Identify suspicious activity.

3\. Review the associated alert or detection search.

4\. Analyze event details and timestamps.

5\. Identify the affected host, account, and source address.

6\. Correlate related events.

7\. Determine whether the activity is suspicious, benign, or inconclusive.

8\. Document investigation findings.

9\. Recommend remediation or escalation.



\## 10. Lab Environment Safety



All activities are performed inside authorized virtual machines using VMware Workstation.



The environment is intended for learning and defensive security investigation.



No production systems or unauthorized external targets are involved.

