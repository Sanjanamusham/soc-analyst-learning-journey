

\# Windows Brute-Force Detection Alert



\## 1. Overview



This alert is designed to identify repeated Windows authentication failures that may indicate brute-force or password-guessing activity.



The detection uses Windows Security Event ID 4625 and a threshold-based approach.



\## 2. Alert Details



| Field | Details |

|---|---|

| Alert Name | Windows Multiple Failed Logons |

| Detection Type | Authentication Monitoring |

| SIEM | Splunk Enterprise |

| Log Source | Windows Security Logs |

| Event ID | 4625 |

| Severity | Medium |

| Detection Threshold | 3 or more failed logons |

| Time Window | 5 minutes |

| Status | Lab Detection |



\## 3. Detection Objective



Identify repeated failed authentication attempts within a short period.



Repeated failed logons may indicate:



\- Brute-force attacks.

\- Password guessing.

\- Incorrect passwords.

\- Account lockout attempts.

\- Application authentication failures.



\## 4. Detection Logic



The detection groups Windows failed logon events by:



\- Time interval.

\- Host.

\- Account.



The alert identifies groups containing three or more failed logon events within a five-minute interval.



\## 5. SPL Detection Query



```spl

index=wineventlog sourcetype="WinEventLog:Security" EventCode=4625

| bin \_time span=5m

| stats count by \_time, host, Account\_Name

| where count >= 3

| sort - count

```



\## 6. Alert Trigger Condition



The detection condition is:



\- Windows Event ID 4625.

\- Three or more failed logons.

\- Events grouped into five-minute intervals.

\- Events grouped by host and account.



When the threshold is met, the activity should be reviewed by the analyst.



\## 7. Analyst Investigation



When an alert is generated:



1\. Identify the affected host.

2\. Identify the targeted account.

3\. Review the source IP address.

4\. Check the number of failed attempts.

5\. Review the authentication failure reason.

6\. Check for successful logons before or after the failures.

7\. Review related security events.

8\. Determine whether the activity is legitimate or suspicious.



\## 8. False Positive Considerations



Possible legitimate causes include:



\- Incorrect password entry.

\- Forgotten passwords.

\- Password changes.

\- Account lockout activity.

\- Misconfigured applications.

\- Automated services using outdated credentials.



The alert should not automatically be classified as a confirmed brute-force attack.



\## 9. Analyst Verdict



The alert is an investigation trigger.



The analyst must validate the activity using the affected account, host, source address, authentication events, and surrounding activity.



\## 10. Recommended Response



If suspicious authentication activity is confirmed:



\- Escalate the incident according to the SOC procedure.

\- Notify the appropriate team.

\- Review the affected account.

\- Investigate the source system.

\- Consider account protection measures according to organizational policy.

\- Document investigation findings.



\## 11. Lab Environment



This detection is developed and tested in an isolated VMware Workstation lab using authorized virtual machines.



No production systems are monitored or targeted.



