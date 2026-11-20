

\# SOC Incident Investigation Report Template



\## 1. Incident Information



| Field | Details |

|---|---|

| Incident ID | |

| Incident Name | |

| Incident Type | |

| Date of Investigation | |

| Analyst | |

| Severity | |

| Status | |

| SIEM | Splunk Enterprise |



\## 2. Incident Summary



Provide a short summary of the security event or alert.



Describe what was detected, which system was affected, and why the activity required investigation.



\## 3. Detection Information



| Field | Details |

|---|---|

| Detection Name | |

| Detection Source | |

| Event ID | |

| Log Source | |

| Detection Time | |

| Affected Host | |

| Account | |

| Source IP Address | |



\## 4. Investigation Objective



Describe the purpose of the investigation.



Explain what the analyst is attempting to determine.



\## 5. Investigation Tools



List the tools used during the investigation.



| Tool | Purpose |

|---|---|

| Splunk Enterprise | Security log search and investigation |

| Windows Event Viewer | Windows event review |

| Linux Logs | Linux authentication investigation |

| VMware Workstation | Isolated virtual lab environment |



\## 6. Investigation Steps



Document the investigation process.



\### Step 1 — Initial Alert Review



Describe the alert and initial observations.



\### Step 2 — Log Analysis



Document the relevant logs and events reviewed.



\### Step 3 — Event Correlation



Describe how related events were correlated.



\### Step 4 — Additional Investigation



Document any additional searches or investigation activities.



\## 7. Evidence



Record the evidence collected during the investigation.



| Evidence ID | Description | Source |

|---|---|---|

| E01 | | |

| E02 | | |

| E03 | | |



Include screenshots, relevant log events, SPL searches, and other supporting evidence.



\## 8. Investigation Findings



| Field | Findings |

|---|---|

| Affected Host | |

| Account | |

| Source IP Address | |

| Event IDs | |

| Event Time | |

| Activity Observed | |

| Authentication Outcome | |

| Related Events | |



\## 9. Analysis



Explain the significance of the observed activity.



Describe whether the activity appears legitimate, suspicious, or malicious.



Include relevant supporting evidence.



\## 10. Incident Verdict



Select the appropriate verdict.



\- \[ ] True Positive — Confirmed suspicious or malicious activity.

\- \[ ] False Positive — Legitimate activity incorrectly identified as suspicious.

\- \[ ] Inconclusive — Insufficient evidence to determine the nature of the activity.



\### Verdict Explanation



Provide the reasoning behind the final verdict.



\## 11. Severity Assessment



| Severity | Description |

|---|---|

| Critical | Severe impact or confirmed high-risk compromise |

| High | Significant security risk requiring urgent investigation |

| Medium | Suspicious activity requiring investigation |

| Low | Limited risk or minor security concern |

| Informational | Activity recorded for monitoring |



\### Assigned Severity



Document the severity and justification.



\## 12. Recommended Response



List the recommended actions based on the investigation findings.



\- Review the affected endpoint.

\- Review the affected account.

\- Investigate related events.

\- Escalate suspicious activity.

\- Apply appropriate remediation according to organizational policy.



\## 13. Lessons Learned



Document lessons learned from the investigation.



Include detection improvements, investigation improvements, and relevant security recommendations.



\## 14. Final Summary



Provide a concise summary of:



\- What happened.

\- What was investigated.

\- What evidence was identified.

\- The final verdict.

\- Recommended actions.



\## 15. Investigation Evidence



List the evidence files and screenshots associated with the incident.



| Evidence | File Name or Location |

|---|---|

| Screenshot 1 | |

| Screenshot 2 | |

| SPL Query | |

| Additional Evidence | |



\## 16. Lab Environment



This report was created as part of an authorized SOC Alert Investigation and Incident Response Lab.



The investigation was performed using an isolated VMware Workstation environment.



