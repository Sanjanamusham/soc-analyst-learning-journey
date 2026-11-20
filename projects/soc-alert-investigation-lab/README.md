# SOC Alert Investigation & Incident Response Lab

## Project Overview

This project demonstrates a hands-on Security Operations Center (SOC) investigation environment built using VMware Workstation and Splunk Enterprise.

The lab simulates security events in isolated Windows and Linux virtual machines, collects endpoint logs using Splunk Universal Forwarders, and investigates suspicious activities using Splunk Search Processing Language (SPL).

The objective is to practice SOC Analyst L1 responsibilities, including alert triage, log analysis, event correlation, incident investigation, identifying potential false positives, determining incident verdicts, and documenting findings.

## Objectives

- Build a multi-source SIEM monitoring environment.
- Collect Windows and Linux security logs.
- Investigate authentication-related security events.
- Identify suspicious login patterns.
- Investigate suspicious PowerShell activity.
- Analyze Linux authentication logs.
- Develop Splunk searches using SPL.
- Create security dashboards and detection alerts.
- Document investigation evidence and findings.
- Practice basic incident response recommendations.

## Lab Environment

| Component | Technology |
|---|---|
| Virtualization | VMware Workstation |
| SIEM | Splunk Enterprise 10.0.1 |
| SIEM Server | Kali Linux |
| Windows Log Source | Windows Server 2022 |
| Linux Log Source | Kali Linux |
| Log Collection | Splunk Universal Forwarder |
| Investigation Language | Splunk SPL |
| Environment | Isolated virtual lab |

## Lab Architecture

The lab consists of a Splunk Enterprise server receiving security logs from Windows and Linux virtual machines through Splunk Universal Forwarders.

Collected events are analyzed using Splunk searches, statistics, dashboards, and scheduled alerts.

The environment was configured and tested within VMware Workstation using isolated virtual machines.

## Investigations

### Incident 01 – Windows Authentication Failure Investigation

**Incident Type:** Suspicious Authentication Activity

**Severity:** Medium – Lab Assessment

**Status:** Investigated

#### Objective

Investigate Windows Security Event ID 4625, identify repeated authentication failures, and determine whether the observed activity represents suspicious authentication behavior.

#### Lab Environment

| Component | Details |
|---|---|
| SIEM | Splunk Enterprise 10.0.1 |
| Endpoint | Windows Server 2022 |
| Log Source | Windows Security Log |
| Event ID | 4625 |
| Index | wineventlog |
| Sourcetype | WinEventLog:Security |
| Forwarder | Splunk Universal Forwarder |
| Environment | Isolated VMware Workstation |

#### Event Description

Windows Security Event ID 4625 records a failed logon attempt.

Repeated authentication failures may indicate:

- Brute-force attempts
- Password guessing
- Incorrect credentials
- Misconfigured applications or services
- Unauthorized authentication attempts

#### Detection Logic

The investigation used a threshold-based detection approach.

- Event ID: 4625
- Threshold: 3 or more failed logons
- Detection window: 5 minutes for the initial threshold investigation
- Grouping: Host and account

#### Investigation Findings

The investigation identified repeated failed authentication events on the Windows endpoint.

The observed events included the following:

- Windows Security Event ID 4625
- Failure reason: Unknown user name or bad password
- Logon types observed: 2 (Interactive) and 7 (Unlock)
- Source addresses included localhost addresses such as `127.0.0.1` and `::1`
- Multiple authentication failures were identified through Splunk statistics and threshold searches.

The source addresses indicate local authentication activity on the endpoint rather than a confirmed external network-based attack.

The detection search was also used to identify account and source-address combinations with three or more failed authentication events within the configured search window.

#### Analyst Verdict

**Verdict: Inconclusive – Suspicious Authentication Activity Observed**

The investigation identified multiple failed authentication attempts within a short period.

However, the observed localhost source addresses and logon types may be associated with legitimate user activity, incorrect credentials, or other local authentication processes.

The available evidence does not conclusively establish that a brute-force attack occurred.

Further investigation would be required to determine whether the activity was authorized or malicious.

#### Recommended Response

- Verify the authentication activity with the account owner.
- Review the affected account and endpoint.
- Check for successful logons following the failures.
- Review related Event IDs 4624 and 4648.
- Investigate additional authentication events and timestamps.
- Escalate suspicious activity to Tier 2 if necessary.
- Follow the organization's incident response procedures.

#### Lessons Learned

- Event ID 4625 is useful for identifying failed authentication attempts.
- Splunk can centralize Windows Security logs.
- Threshold-based searches help identify repeated authentication failures.
- Detection results require investigation before classifying an incident.
- Source addresses, account names, and logon types provide useful investigation context.

---

### Incident 02 – Authentication Anomaly Investigation

**Objective:** Correlate failed and successful logon events to investigate suspicious authentication activity.

The investigation focused on reviewing authentication events and identifying patterns involving failed and successful logons.

The objective was to understand the authentication sequence and determine whether the observed activity required further investigation.

**Skills Practiced:**

- Windows authentication event analysis
- Event correlation
- Failed and successful logon investigation
- Account activity review
- Basic alert triage

---

### Incident 03 – Suspicious PowerShell Activity Investigation

**Objective:** Investigate controlled PowerShell execution and identify relevant endpoint telemetry.

The investigation involved examining PowerShell-related activity in the Windows environment and reviewing relevant logs to understand command execution behavior.

**Skills Practiced:**

- Windows endpoint investigation
- PowerShell activity analysis
- Security event log review
- Identifying suspicious command execution
- Investigative documentation

---

### Incident 04 – Linux Authentication Investigation

**Objective:** Analyze Linux authentication logs and investigate suspicious login activity.

The investigation focused on Linux authentication telemetry and identifying relevant login-related events.

**Skills Practiced:**

- Linux authentication log analysis
- SSH authentication investigation
- Failed login identification
- Linux endpoint monitoring
- Basic incident investigation

---

## Splunk Monitoring and Dashboards

The lab includes Splunk monitoring dashboards designed to provide visibility into endpoint activity and authentication events.

The dashboards include:

- Windows failed logon monitoring
- Windows successful logon monitoring
- Windows authentication failure trends
- Linux log source activity
- Monitored host overview
- Splunk data source inventory

The dashboards help visualize security events and support investigation and monitoring activities.

## Alert Configuration

### Alert 01 – Windows Multiple Failed Logons

**Alert Name:** Windows Multiple Failed Logons

**Alert Type:** Scheduled

**Schedule:** Hourly, at 15 minutes past the hour

**Detection Source:** Windows Security Event ID 4625

**Threshold:** 3 or more failed authentication events

**Search Window:** Last 60 minutes

**Severity:** Medium

**Trigger Action:** Add to Triggered Alerts

**Status:** Configured and Enabled

#### Detection Query

```spl
index=wineventlog EventCode=4625 earliest=-60m latest=now
| stats count by host Account_Name Source_Network_Address
| where count >= 3
```

#### Detection Validation

The detection search was manually executed in Splunk and returned results containing account, host, source-address, and failed-authentication counts.

The results included multiple combinations meeting the configured threshold of three or more events.

The scheduled alert was saved and enabled in Splunk.

**Scheduled alert firing is pending verification.** The manually executed search validates the detection query, but scheduled execution has not yet been confirmed.

#### Evidence

- `07-windows-failed-logon-alert-configuration.png`
- `08-windows-failed-logon-detection-results.png`

## Skills Demonstrated

- SIEM monitoring
- Splunk Enterprise
- Log ingestion and analysis
- Windows Security Event Logs
- Linux authentication logs
- Splunk Search Processing Language (SPL)
- Authentication investigation
- Event correlation
- Alert triage
- Detection logic validation
- Dashboard development
- Incident documentation
- Basic incident response
- Git and GitHub documentation

## Safety

All security simulations were performed using authorized virtual machines in a controlled laboratory environment.

No real accounts, production systems, public targets, or destructive malware were used.

## Project Status

- [x] Splunk configuration verification
- [x] Windows log ingestion
- [x] Linux log ingestion
- [x] Incident 01 – Windows authentication failure investigation
- [x] Incident 02 – Authentication anomaly investigation
- [x] Incident 03 – PowerShell activity investigation
- [x] Incident 04 – Linux authentication investigation
- [x] Dashboard development
- [x] Detection search validation
- [x] VMware environment validation
- [x] Project screenshots
- [x] GitHub documentation
- [x] Alert 01 configuration
- [ ] Scheduled alert firing verification
- [ ] Final incident report review
- [ ] Final GitHub repository review

## Conclusion

This project provided practical experience in building a SIEM monitoring environment, collecting endpoint logs, investigating authentication events, analyzing suspicious activity, developing detection searches, creating dashboards, configuring alerts, and documenting investigation findings.

The lab demonstrates foundational SOC Analyst L1 skills in security monitoring, log analysis, alert triage, investigation, and basic incident response within a controlled virtual environment.
