

\# Suspicious Authentication Activity Alert



\## 1. Overview



This alert is intended to identify potentially suspicious Windows authentication activity for further SOC investigation.



Authentication events are reviewed to identify unusual login behavior, failed authentication attempts, and successful logons that may require additional investigation.



\## 2. Alert Details



| Field | Details |

|---|---|

| Alert Name | Suspicious Windows Authentication Activity |

| Detection Type | Authentication Monitoring |

| SIEM | Splunk Enterprise |

| Log Source | Windows Security Logs |

| Event IDs | 4624, 4625, 4648 |

| Severity | Medium - Investigation |

| Status | Lab Detection |



\## 3. Event IDs



| Event ID | Description |

|---|---|

| 4624 | Successful logon |

| 4625 | Failed logon |

| 4648 | Logon using explicit credentials |



These events provide information about Windows authentication activity.



\## 4. Detection Objective



Identify authentication activity that requires further investigation.



Examples include:



\- Repeated failed logons.

\- Successful logons following repeated failures.

\- Authentication using explicit credentials.

\- Unexpected accounts.

\- Unusual source addresses.

\- Unexpected logon types.

\- Authentication activity outside expected patterns.



\## 5. Detection Search



The following search retrieves relevant authentication events.



```spl

index=wineventlog sourcetype="WinEventLog:Security" (EventCode=4624 OR EventCode=4625 OR EventCode=4648)

| table \_time host EventCode Account\_Name TargetUserName Source\_Network\_Address IpAddress Logon\_Type

| sort - \_time

```



\## 6. Investigation Fields



The analyst should review:



| Field | Investigation Purpose |

|---|---|

| \_time | Determine when the event occurred |

| host | Identify the affected system |

| EventCode | Identify the authentication event |

| Account\_Name | Identify the account involved |

| TargetUserName | Identify the targeted username |

| Source\_Network\_Address | Identify the source address |

| IpAddress | Review the available IP address field |

| Logon\_Type | Understand the type of logon |



\## 7. Investigation Workflow



1\. Review the authentication event.

2\. Identify the affected host and account.

3\. Review the source address.

4\. Identify the logon type.

5\. Search for related failed authentication events.

6\. Search for successful authentication events.

7\. Review the timeline.

8\. Determine whether the activity is expected.

9\. Document the investigation verdict.



\## 8. False Positive Considerations



Suspicious authentication detections may include legitimate activity such as:



\- Users entering incorrect passwords.

\- Administrator activity.

\- Service account authentication.

\- Local interactive logons.

\- Application authentication.

\- Credential-related configuration issues.



Authentication activity must be reviewed in context.



\## 9. Analyst Verdict



The detection identifies potentially suspicious authentication events.



The presence of an authentication event does not automatically confirm malicious activity.



The analyst must correlate the event with other available evidence before classifying the activity.



\## 10. Recommended Response



If suspicious activity is identified:



\- Review the account and endpoint.

\- Investigate related authentication events.

\- Check for unusual activity.

\- Escalate confirmed suspicious behavior.

\- Document the investigation and evidence.



\## 11. Lab Environment



This detection is intended for authorized security monitoring and investigation in an isolated VMware Workstation environment.



