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

### Incident 01 – Windows Failed Authentication Investigation

**Status:** Evidence reviewed and documentation updated  
**Verdict:** Inconclusive — Local Failed Authentication Activity Observed

A Splunk search for Windows Security Event ID 4625 returned **8 raw events** in the selected Last 24 Hours range.

Verified findings:

- Host: `WIN-TU878J0IPCG`
- Failed target accounts: `soctest` (5 events) and `DELL` (3 events)
- Source addresses: `::1` and `127.0.0.1` (local loopback)
- Logon types: 2 (Interactive) and 7 (Unlock)
- Failure status: `0xC000006D`
- Failure sub-status: `0xC000006A` (incorrect password)
- Caller process: `C:\\Windows\\System32\\svchost.exe`

The raw event messages were reviewed. Splunk extracted both the Subject account and failed target account into multivalue fields, so grouping directly by `Account_Name` inflated counts. The raw event count (8) was used as the verified total.

The evidence shows local failed authentication activity. No external source IP or confirmed brute-force attack was identified. The underlying cause remains unconfirmed.

See [Incident 01 report](investigations/incident-01-brute-force/README.md) and [validated SPL queries](investigations/incident-01-brute-force/spl-queries.md).

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

**Status: Completed and reviewed.** Dashboard was created, screenshots were captured/shared, and dashboard documentation is present in the repository. No dashboard recreation is required.

The lab includes Splunk monitoring dashboards designed to provide visibility into endpoint activity and authentication events.

The dashboards include:

- Windows failed logon monitoring
- Windows successful logon monitoring
- Windows authentication failure trends
- Linux log source activity
- Monitored host overview
- Splunk data source inventory

The dashboards help visualize security events and support investigation and monitoring activities. Dashboard creation, screenshots, and the documented dashboard work are considered completed based on the previously shared evidence.

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

**Status: Configuration completed.** The scheduled alert was configured, saved, and enabled. The detection search was manually validated, and configuration/results screenshots were captured. Scheduled notification/trigger firing is an optional additional verification and is not required to claim alert configuration completed.

#### Detection Query

```spl
index=wineventlog sourcetype="WinEventLog:Security" EventCode=4625 earliest=-60m latest=now
| eval Failed_Account=mvindex(Account_Name,1)
| stats count by host Failed_Account Source_Network_Address
| where count >= 3
```

#### Detection Validation

The detection search was manually executed in Splunk and returned results containing account, host, source-address, and failed-authentication counts.

The results included multiple combinations meeting the configured threshold of three or more events.

The scheduled alert was saved and enabled in Splunk. The detection search was manually run and validated against the available event data.

The configuration and manual detection results are documented in the captured evidence. A separate scheduled alert-trigger notification was not captured. The project claims alert configuration and manual detection validation—not notification delivery.

#### Evidence

- `07-windows-failed-logon-alert-configuration.png`
- `08-windows-failed-logon-detection-results.png`

## Project Completion Checklist — Core Portfolio Scope

- [x] Multi-source log ingestion verified
- [x] Incident 01 investigated and documented using raw evidence
- [x] Incident 01 SPL corrected for observed multivalue extraction
- [x] Failed-logon detection search manually validated
- [x] Scheduled alert configured, saved, and enabled
- [x] Dashboard created, reviewed, and screenshots captured
- [x] Alert configuration and detection-result screenshots captured
- [x] Project documentation reviewed and aligned with evidence

**Core portfolio status: Completed.**

### Optional Extensions (Not Required for Core Completion)

- Scheduled alert trigger/notification delivery verification (configuration is completed; delivery was not separately captured)
- Additional evidence-backed investigations: Incident 02 authentication correlation, Incident 03 PowerShell, and Incident 04 Linux authentication
- Optional screenshot bundle organization or additional report polish

These extensions are intentionally not marked as unchecked blockers. Incident 02–04 documentation currently serves as investigation guides unless separate evidence/findings are added.

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

### Core Portfolio — Completed

- [x] Splunk log collection confirmed for Kali syslog and Windows Application, Security, and System logs
- [x] Incident 01 raw Event ID 4625 evidence reviewed
- [x] Incident 01 findings and verdict documented
- [x] Incident 01 SPL corrected for observed multivalue account extraction
- [x] Failed-logon detection search manually validated
- [x] Alert configured, saved, and enabled
- [x] Alert configuration and detection-result screenshots reviewed
- [x] Dashboard functionality and screenshots reviewed
- [x] Core project documentation reviewed and aligned with evidence

### Optional Extensions — Not Blocking Core Completion

- Scheduled notification/trigger delivery verification (alert configuration is completed; separate delivery evidence was not captured)
- Evidence-backed case studies for Incidents 02–04 (current documents are investigation guides)
- Optional final screenshot bundle organization and additional report polish

**Core portfolio status: Completed.** Optional extensions are not marked as pending project requirements.

## Conclusion

This core portfolio project is completed: multi-source log ingestion, an evidence-backed Windows failed-authentication investigation, dashboard creation and review, alert configuration, manual detection-search validation, and documentation are complete. Optional extensions may add scheduled notification-delivery evidence and further Incident 02–04 case studies, but they do not block the core project completion claim.
