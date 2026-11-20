

\# Incident 02 — Windows Authentication Anomaly Investigation



\## 1. Incident Overview



| Field | Details |

|---|---|

| Incident Name | Windows Authentication Anomaly |

| Incident Type | Authentication Monitoring |

| Severity | Investigation Required |

| Status | Lab Investigation |

| SIEM | Splunk Enterprise |

| Endpoint | Windows Server 2022 |

| Log Source | Windows Security Logs |

| Environment | Isolated VMware Workstation Lab |



\## 2. Objective



Investigate Windows authentication events to identify potentially suspicious login behavior.



The investigation focuses on reviewing authentication events, identifying unusual patterns, and correlating related events.



\## 3. Relevant Windows Event IDs



| Event ID | Description |

|---|---|

| 4624 | Successful logon |

| 4625 | Failed logon |

| 4648 | Logon using explicit credentials |



These events help analysts investigate authentication activity.



\## 4. Investigation Questions



The investigation should answer:



\- Which account was involved?

\- Which host generated the event?

\- When did the activity occur?

\- Was the authentication successful or unsuccessful?

\- What was the source address?

\- What was the logon type?

\- Were there repeated authentication attempts?

\- Was there a successful logon after failed attempts?

\- Was the activity expected?



\## 5. Investigation Process



\### Step 1 — Identify Authentication Events



Search the Windows Security index for relevant authentication events.



\### Step 2 — Review Event Details



Review the event timestamp, host, username, event ID, source address, and logon type.



\### Step 3 — Identify Patterns



Look for repeated failed logons, unexpected successful logons, and authentication activity involving unusual accounts.



\### Step 4 — Correlate Events



Compare failed and successful authentication events to establish a timeline.



\### Step 5 — Determine the Verdict



Classify the investigation based on the available evidence.



Possible verdicts include:



\- True Positive — Confirmed suspicious or malicious activity.

\- False Positive — Activity is explained by legitimate behavior.

\- Inconclusive — Available evidence is insufficient to determine the nature of the activity.



\## 6. Investigation Findings



The investigation findings should be recorded using verified Splunk search results and screenshots.



| Field | Finding |

|---|---|

| Affected Host | To be documented from verified evidence |

| Account | To be documented from verified evidence |

| Event ID | To be documented from verified evidence |

| Source Address | To be documented from verified evidence |

| Logon Type | To be documented from verified evidence |

| Event Time | To be documented from verified evidence |

| Authentication Outcome | To be documented from verified evidence |



\## 7. Analysis



Authentication anomalies require investigation because unusual login behavior may indicate account misuse or unauthorized access.



However, unusual authentication activity can also result from legitimate user behavior, configuration problems, or administrative actions.



The analyst must correlate the authentication events with other available evidence before reaching a conclusion.



\## 8. Analyst Verdict



\*\*Verdict: Pending Evidence Review\*\*



The final verdict should be updated after reviewing the actual investigation results.



Do not classify the activity as malicious without supporting evidence.



\## 9. Recommended Response



Depending on the investigation findings:



1\. Review the affected account.

2\. Review the endpoint.

3\. Check related authentication events.

4\. Investigate the source address.

5\. Review suspicious activity before and after the authentication event.

6\. Escalate confirmed suspicious activity.

7\. Document the investigation.



\## 10. Lessons Learned



\- Authentication events provide valuable investigation information.

\- Event correlation improves investigation accuracy.

\- Successful and failed logons should be reviewed together.

\- Source addresses and logon types provide important context.

\- Detection alerts require analyst validation.

\- Evidence should support the final incident verdict.



\## 11. Evidence



Investigation screenshots should be maintained in the incident screenshots directory.



Evidence should include relevant Splunk searches, authentication event details, and investigation results.



\## 12. Lab Safety



The investigation is performed in an isolated VMware Workstation lab using authorized virtual machines.



