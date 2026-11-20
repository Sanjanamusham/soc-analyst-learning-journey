\# Windows Splunk Universal Forwarder Configuration



\## 1. Overview



The Splunk Universal Forwarder is installed on the Windows Server 2022 virtual machine to collect Windows Security logs and forward them to Splunk Enterprise.



The forwarder enables centralized monitoring and investigation of Windows authentication events.



\## 2. Environment



| Component | Details |

|---|---|

| Operating System | Windows Server 2022 |

| Log Source | Windows Security |

| SIEM | Splunk Enterprise |

| Forwarder | Splunk Universal Forwarder |

| Environment | VMware Workstation |



\## 3. Purpose



The Windows Universal Forwarder collects security-related events from the Windows endpoint.



These events are used for:



\- Authentication failure investigation.

\- Successful logon monitoring.

\- Suspicious authentication detection.

\- Event correlation.

\- Security incident investigation.



\## 4. Windows Security Events



The following Windows Security events are relevant to this lab:



| Event ID | Description |

|---|---|

| 4624 | Successful logon |

| 4625 | Failed logon |

| 4648 | Logon using explicit credentials |



Event ID 4625 is particularly important for investigating repeated failed authentication attempts.



\## 5. Log Collection Process



The collection process follows these steps:



1\. Windows generates Security events.

2\. Splunk Universal Forwarder monitors configured log sources.

3\. The forwarder sends collected events to Splunk Enterprise.

4\. Splunk indexes the received events.

5\. The analyst searches and investigates the collected events.



\## 6. Verification



Windows log ingestion was verified through Splunk Search \& Reporting.



The investigation confirmed that Windows Security events were available for searching.



The following activities were verified:



\- Windows Security event ingestion.

\- Failed logon event investigation.

\- Successful logon event investigation.

\- Event ID 4625 search.

\- Authentication event statistics.

\- Windows authentication dashboards.



\## 7. Troubleshooting



If Windows events are not visible in Splunk:



1\. Confirm the Windows virtual machine is running.

2\. Confirm the Splunk Universal Forwarder service is running.

3\. Verify the forwarder's configured destination.

4\. Verify network connectivity between the endpoint and Splunk server.

5\. Confirm the Windows Security log is being collected.

6\. Verify the correct Splunk index is selected.

7\. Check the search time range.

8\. Search for the relevant host and sourcetype.



\## 8. Evidence



Windows log ingestion and investigation evidence are stored in the project screenshots directory.



Relevant screenshots include:



\- Splunk data inventory.

\- Windows failed logon events.

\- Windows successful logon dashboard.

\- Windows authentication failure trend.

\- Windows brute-force investigation.

