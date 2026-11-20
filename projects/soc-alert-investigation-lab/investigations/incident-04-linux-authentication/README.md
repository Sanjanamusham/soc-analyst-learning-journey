

\# Incident 04 — Linux Authentication Investigation



\## 1. Incident Overview



| Field | Details |

|---|---|

| Incident Name | Linux Authentication Investigation |

| Incident Type | Authentication Monitoring |

| Severity | Investigation Required |

| Status | Lab Investigation |

| SIEM | Splunk Enterprise |

| Log Source | Linux Authentication Logs |

| Environment | Isolated VMware Workstation Lab |



\## 2. Objective



Investigate Linux authentication logs to identify potentially suspicious login activity.



The investigation focuses on reviewing authentication failures, successful logins, usernames, source addresses, and repeated authentication attempts.



\## 3. Linux Authentication Logs



Linux authentication logs provide information about authentication activity.



Depending on the Linux distribution, authentication information may be available in:



\- `/var/log/auth.log`

\- `/var/log/secure`

\- System journal logs



These logs may contain information about:



\- SSH authentication attempts.

\- Failed logins.

\- Successful logins.

\- Invalid usernames.

\- Authentication failures.

\- Account activity.



\## 4. Investigation Objectives



The investigation should identify:



\- Authentication failures.

\- Repeated failed login attempts.

\- Invalid usernames.

\- Successful logins.

\- Source IP addresses.

\- Target usernames.

\- Authentication timestamps.

\- Potential suspicious authentication patterns.



\## 5. Investigation Process



\### Step 1 — Search Linux Authentication Events



Search the collected Linux authentication logs in Splunk.



\### Step 2 — Review Authentication Details



Review the timestamp, username, source address, and authentication outcome.



\### Step 3 — Identify Repeated Failures



Look for repeated authentication failures associated with the same account or source address.



\### Step 4 — Review Successful Logins



Identify successful authentication events and determine whether they are related to previous failures.



\### Step 5 — Correlate Activity



Correlate authentication events by username, source address, and time.



\### Step 6 — Determine the Verdict



Classify the activity based on the available evidence.



\## 6. Investigation Findings



The investigation findings should be documented using verified Splunk search results.



| Field | Finding |

|---|---|

| Linux Host | To be documented from verified evidence |

| Username | To be documented from verified evidence |

| Source Address | To be documented from verified evidence |

| Authentication Outcome | To be documented from verified evidence |

| Event Time | To be documented from verified evidence |

| Number of Attempts | To be documented from verified evidence |

| Related Activity | To be documented from verified evidence |



\## 7. Analysis



Repeated Linux authentication failures may indicate:



\- Password guessing.

\- Brute-force activity.

\- Incorrect credentials.

\- Misconfigured services.

\- Legitimate user login problems.



The analyst should investigate the source address, targeted account, frequency of attempts, and related successful logins.



Authentication failures alone do not confirm a brute-force attack.



\## 8. Analyst Verdict



\*\*Verdict: Pending Evidence Review\*\*



The final verdict should be updated after reviewing the actual Linux authentication events collected in Splunk.



The activity should not be classified as malicious without supporting evidence.



\## 9. Recommended Response



If suspicious authentication activity is identified:



1\. Identify the source address.

2\. Identify the targeted username.

3\. Review the number and frequency of attempts.

4\. Check for successful logins.

5\. Review other activity from the source.

6\. Investigate the affected Linux endpoint.

7\. Escalate confirmed suspicious activity.

8\. Document investigation findings.



\## 10. Lessons Learned



\- Linux authentication logs are useful for security monitoring.

\- Repeated authentication failures may indicate suspicious activity.

\- Source IP addresses provide important investigation context.

\- Successful and failed logins should be correlated.

\- Authentication activity requires analyst validation.

\- Evidence should support the incident verdict.



\## 11. Evidence



Investigation screenshots should be maintained in the incident screenshots directory.



Evidence should include relevant Splunk searches, Linux authentication events, and investigation results.



\## 12. Lab Safety



This investigation is performed in an isolated VMware Workstation environment using authorized virtual machines.



