

\# Incident 03 — PowerShell Activity Investigation



\## 1. Incident Overview



| Field | Details |

|---|---|

| Incident Name | PowerShell Activity Investigation |

| Incident Type | Endpoint Activity Monitoring |

| Severity | Investigation Required |

| Status | Lab Investigation |

| SIEM | Splunk Enterprise |

| Endpoint | Windows Server 2022 |

| Log Source | Windows PowerShell Logs |

| Environment | Isolated VMware Workstation Lab |



\## 2. Objective



Investigate PowerShell activity on a Windows endpoint using security logs collected by Splunk.



PowerShell is a legitimate Windows scripting and automation tool.



However, attackers may also use PowerShell to execute commands, automate malicious activity, download files, or perform reconnaissance.



The objective is to identify suspicious PowerShell activity and determine whether it requires further investigation.



\## 3. Relevant Windows Logs



\### PowerShell Operational Log



The PowerShell Operational log can provide information about PowerShell activity.



Important event IDs include:



| Event ID | Description |

|---|---|

| 4103 | Module logging |

| 4104 | Script block logging |



Event ID 4104 can contain script block content when script block logging is enabled.



The availability of these events depends on the Windows logging configuration.



\### Windows Security Log



Windows Security Event ID 4688 records process creation when the appropriate auditing configuration is enabled.



Process creation events may help identify PowerShell execution.



\## 4. Investigation Objectives



The investigation focuses on:



\- Identifying PowerShell execution.

\- Reviewing command-line activity.

\- Identifying the executing account.

\- Reviewing timestamps.

\- Identifying suspicious command patterns.

\- Investigating encoded commands.

\- Reviewing suspicious download or execution activity.

\- Correlating PowerShell activity with other endpoint events.



\## 5. Investigation Process



\### Step 1 — Search PowerShell Events



Search collected PowerShell-related logs in Splunk.



\### Step 2 — Review Event Details



Review the timestamp, host, account, event ID, and available script or command information.



\### Step 3 — Identify Suspicious Patterns



Review commands for suspicious characteristics such as:



\- Encoded commands.

\- Unusual execution parameters.

\- Download-related commands.

\- Unexpected script execution.

\- Suspicious file paths.

\- Unusual process activity.



\### Step 4 — Correlate Events



Correlate PowerShell activity with other available endpoint events.



\### Step 5 — Determine the Verdict



Determine whether the activity is legitimate, suspicious, malicious, or inconclusive based on the available evidence.



\## 6. Investigation Findings



The investigation findings should be recorded using verified Splunk results and screenshots.



| Field | Finding |

|---|---|

| Affected Host | To be documented from verified evidence |

| Account | To be documented from verified evidence |

| Event ID | To be documented from verified evidence |

| Process | To be documented from verified evidence |

| Command or Script | To be documented from verified evidence |

| Event Time | To be documented from verified evidence |

| Activity | To be documented from verified evidence |



\## 7. Analysis



PowerShell activity is not automatically malicious.



Legitimate administrators and applications use PowerShell for system management and automation.



The analyst should evaluate the command, execution context, account, host, timestamp, and related events before classifying the activity.



\## 8. Analyst Verdict



\*\*Verdict: Pending Evidence Review\*\*



The final verdict must be based on the actual PowerShell activity observed in the lab.



Do not classify legitimate PowerShell execution as malicious without supporting evidence.



\## 9. Recommended Response



If suspicious PowerShell activity is identified:



1\. Identify the affected endpoint.

2\. Identify the account executing PowerShell.

3\. Review the command or script.

4\. Investigate related processes.

5\. Review associated network activity if available.

6\. Correlate with other security events.

7\. Escalate confirmed suspicious activity.

8\. Document findings and evidence.



\## 10. Lessons Learned



\- PowerShell is a legitimate administration tool.

\- PowerShell can also be abused by attackers.

\- Script block logging can provide useful investigation evidence.

\- Process creation logging can help identify execution activity.

\- Command-line analysis is important for endpoint investigations.

\- Activity must be reviewed in context.

\- Evidence is required to support the incident verdict.



\## 11. Evidence



Investigation screenshots should be maintained in the incident screenshots directory.



Evidence should include relevant Splunk searches, event details, and investigation results.



\## 12. Lab Safety



This investigation is performed in an isolated VMware Workstation lab using authorized virtual machines.



All investigation activity is limited to the controlled environment.



