\# Linux Splunk Log Collection



\## 1. Overview



Linux log collection is included in the SOC Alert Investigation and Incident Response Lab to practice monitoring and investigating Linux authentication activity.



The Linux environment is monitored using Splunk log collection capabilities.



\## 2. Environment



| Component | Details |

|---|---|

| Operating System | Kali Linux |

| SIEM | Splunk Enterprise |

| Log Source | Linux system and authentication logs |

| Virtualization | VMware Workstation |

| Environment | Isolated Virtual Lab |



\## 3. Objective



The objective is to collect Linux log data and use Splunk to investigate authentication-related activity.



The investigation focuses on:



\- Linux authentication logs.

\- Login activity.

\- Authentication failures.

\- Log source monitoring.

\- Suspicious login patterns.



\## 4. Linux Log Sources



Linux system logs contain information about system activity and authentication events.



Authentication-related log information can help analysts investigate:



\- Failed login attempts.

\- Successful login activity.

\- User authentication.

\- SSH authentication activity.

\- Suspicious account activity.



\## 5. Log Collection Process



1\. Linux generates system and authentication log events.

2\. Configured log collection sends the events to Splunk.

3\. Splunk indexes the incoming data.

4\. The analyst searches Linux log events.

5\. Authentication activity is reviewed and investigated.



\## 6. Verification



Linux log source activity was verified using Splunk.



The Linux log source activity dashboard screenshot is maintained in the project screenshots directory.



\## 7. Investigation



Linux authentication logs are used to identify suspicious authentication patterns.



The investigation process includes:



\- Reviewing event timestamps.

\- Identifying authentication-related messages.

\- Identifying usernames.

\- Reviewing login outcomes.

\- Investigating repeated failures.

\- Documenting findings.



\## 8. Troubleshooting



If Linux events are not visible in Splunk:



1\. Verify the Linux virtual machine is running.

2\. Verify the log collection service or forwarder is running.

3\. Confirm the configured log source.

4\. Verify network connectivity.

5\. Confirm the data is reaching Splunk.

6\. Check the selected index and time range.

7\. Review the available sourcetypes.



\## 9. Evidence



Linux monitoring evidence is maintained in the screenshots directory.



The available evidence includes the Linux log source activity dashboard.

