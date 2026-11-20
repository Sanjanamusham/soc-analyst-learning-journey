\# Incident 01 — Windows Failed Logon Investigation



\## 1. Incident Overview



| Field | Details |

|---|---|

| Incident Name | Windows Authentication Failure Investigation |

| Incident Type | Suspicious Authentication Activity |

| Severity | Medium - Lab Assessment |

| Status | Investigated |

| SIEM | Splunk Enterprise |

| Endpoint | Windows Server 2022 |

| Event ID | 4625 |

| Index | wineventlog |

| Environment | Isolated VMware Workstation Lab |



\## 2. Objective



Investigate repeated Windows failed logon events and determine whether the activity indicates suspicious authentication behavior.



The investigation uses Windows Security Event ID 4625.



\## 3. Event Description



Windows Security Event ID 4625 records a failed logon attempt.



Repeated authentication failures may indicate:



\- Brute-force attempts.

\- Password guessing.

\- Incorrect credentials.

\- Misconfigured applications or services.

\- Unauthorized authentication attempts.



\## 4. Detection Logic



The investigation uses a threshold-based detection.



| Detection Parameter | Value |

|---|---|

| Event ID | 4625 |

| Threshold | 3 or more failures |

| Time Window | 5 minutes |

| Grouping | Host and account |



The detection search identifies repeated authentication failures within the configured time interval.



\## 5. Investigation Findings



The Splunk investigation identified multiple failed authentication events.



The findings included:



\- Affected host: WIN-TU878J0IPCG

\- Observed accounts: DELL and WIN-TU878J0IPCGS

\- Source addresses: 127.0.0.1 and ::1

\- Event ID: 4625

\- Logon types observed: 2 and 7

\- Failure reason: Unknown user name or bad password



The investigation identified repeated failed logons exceeding the configured threshold.



The observed source addresses were loopback addresses, indicating local authentication activity on the endpoint rather than an external source IP address.



\## 6. Analysis



Repeated failed authentication attempts can indicate suspicious activity.



However, the observed authentication failures originated from local loopback addresses.



The activity may be associated with:



\- Incorrect credentials.

\- Local interactive authentication.

\- User account unlock attempts.

\- Local application authentication.

\- Potentially suspicious authentication behavior.



The available evidence does not conclusively establish that the activity was a brute-force attack.



\## 7. Analyst Verdict



\*\*Verdict: Inconclusive — Suspicious Authentication Activity Observed\*\*



The detection identified multiple failed logon events within a short period.



The threshold was exceeded, but the source addresses were local loopback addresses.



Additional investigation would be required to determine whether the activity was legitimate or malicious.



\## 8. Recommended Response



A SOC Analyst should:



1\. Review the affected account.

2\. Verify whether the activity was expected.

3\. Review the source workstation.

4\. Investigate successful logons before and after the failures.

5\. Review related authentication events.

6\. Check for other suspicious activity on the endpoint.

7\. Escalate if suspicious behavior cannot be explained.



\## 9. Lessons Learned



\- Event ID 4625 is useful for investigating authentication failures.

\- Threshold-based detections identify repeated activity.

\- Source addresses provide important investigation context.

\- Detection results require analyst validation.

\- Local authentication failures should not automatically be classified as external brute-force attacks.

\- Context is necessary to determine the correct incident verdict.



\## 10. Evidence



Evidence is maintained in the incident screenshots directory.



The evidence includes:



\- Windows Event Viewer Event ID 4625.

\- Splunk failed authentication events.

\- Authentication statistics.

\- Threshold detection results.

\- Investigation details.



\## 11. Lab Safety



This investigation was performed using authorized Windows virtual machines in an isolated VMware Workstation environment.



No production systems or unauthorized accounts were targeted.

