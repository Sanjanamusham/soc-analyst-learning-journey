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

**Status: Dashboard created and documented.** Dashboard screenshots and documentation were previously committed. Final review of the dashboard panels and screenshot evidence remains part of portfolio quality review.

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

**Status:** Alert configured and saved; manual detection search validated; scheduled firing not yet verified

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

**Scheduled alert firing is pending verification.** The manually executed search validates the detection query, but scheduled execution has not yet been confirmed.

#### Evidence

- `07-windows-failed-logon-alert-configuration.png`
- `08-windows-failed-logon-detection-results.png`

## Project Completion Checklist

- [x] Multi-source log ingestion verified
- [x] Incident 01 investigated and documented using raw evidence
- [x] Dashboard created and documented
- [x] Alert configured and detection search manually validated
- [ ] Scheduled alert firing verified
- [ ] Incidents 02–04 completed with evidence-backed findings
- [ ] Final screenshots and full project review

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

- [x] Splunk log collection confirmed for Kali syslog and Windows Application, Security, and System logs
- [x] Incident 01 raw Event ID 4625 evidence reviewed
- [x] Incident 01 findings and verdict documented
- [x] Incident 01 SPL corrected for observed multivalue account extraction
- [ ] Re-run corrected five-minute threshold search and verify result
- [ ] Verify scheduled alert firing
- [ ] Complete evidence-backed investigations for Incidents 02–04
- [ ] Validate dashboard functionality and screenshots
- [ ] Final project review

## Conclusion

This project is a hands-on SOC learning lab. Confirmed work includes multi-source log ingestion and an evidence-backed Windows failed-authentication investigation. Remaining detections, dashboards, and investigations should be marked complete only after their behavior and evidence are verified in the lab.
