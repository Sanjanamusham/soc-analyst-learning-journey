\# SOC Lab Monitoring Dashboard



\## Overview



This dashboard was developed using Splunk Enterprise to monitor security events collected from Windows and Linux virtual machines in an isolated VMware Workstation environment.



The dashboard provides a centralized overview of authentication activity, Windows Security events, Linux log sources, and monitored endpoints.



\## Dashboard Components



\### 1. Windows Failed Logon Activity



\*\*Event ID:\*\* 4625



Displays failed authentication events grouped by host, account, and source network address.



\*\*Purpose:\*\*

\- Identify repeated authentication failures.

\- Monitor suspicious account activity.

\- Support brute-force detection investigations.



\### 2. Windows Successful Logons



\*\*Event ID:\*\* 4624



Displays successful authentication events grouped by host, account, and logon type.



\*\*Purpose:\*\*

\- Monitor successful authentication activity.

\- Correlate successful logons with previous failures.

\- Identify unusual authentication patterns.



\### 3. Windows Authentication Failure Trend



Displays Windows failed logon events over time.



\*\*Purpose:\*\*

\- Identify periods of increased authentication failures.

\- Observe authentication activity patterns.

\- Support time-based security investigations.



\### 4. Linux Log Source Activity



Displays Linux log sources collected by Splunk.



\*\*Purpose:\*\*

\- Verify Linux log ingestion.

\- Monitor available log sources.

\- Identify monitored Linux endpoints.



\### 5. Monitored Hosts and Log Sources



Displays event counts grouped by host, index, and sourcetype.



\*\*Purpose:\*\*

\- Monitor centralized log collection.

\- Verify multiple endpoints are sending events.

\- Identify active data sources.



\## Technologies Used



\- Splunk Enterprise 10.0.1

\- Splunk Search Processing Language (SPL)

\- Windows Server 2022

\- Kali Linux

\- Splunk Universal Forwarder

\- Splunk Linux Forwarder

\- VMware Workstation



\## Skills Demonstrated



\- SIEM dashboard development

\- SPL search and aggregation

\- Windows Security Event Log monitoring

\- Linux log monitoring

\- Authentication event analysis

\- Log source validation

\- Endpoint monitoring

\- Security monitoring and visualization



\## Environment



All monitoring activities were performed using authorized virtual machines in an isolated VMware Workstation laboratory environment.



No production systems or unauthorized targets were involved.

