# SOC Alert Investigation & Incident Response Lab

## Project Overview

This project demonstrates a hands-on Security Operations Center (SOC) investigation environment built using VMware Workstation and Splunk Enterprise.

The lab simulates security events in isolated Windows and Linux virtual machines, collects endpoint logs using Splunk Universal Forwarders, and investigates suspicious activities using Splunk Search Processing Language (SPL).

The objective is to practice the responsibilities of a SOC Analyst L1, including alert triage, log analysis, event correlation, incident investigation, determining True Positive or False Positive verdicts, and documenting findings.

## Objectives

- Build a multi-source SIEM monitoring environment.
- Collect Windows and Linux security logs.
- Investigate authentication-related security events.
- Identify suspicious login patterns.
- Investigate suspicious PowerShell activity.
- Analyze Linux authentication logs.
- Develop Splunk searches for security investigations.
- Create security alerts and dashboards.
- Document investigation evidence and incident verdicts.
- Practice incident response recommendations.

## Lab Environment

| Component              | Technology                 |
| ---------------------- | -------------------------- |
| Virtualization         | VMware Workstation         |
| SIEM                   | Splunk Enterprise          |
| SIEM Server            | Kali Linux                 |
| Windows Log Source     | Windows Server 2022        |
| Linux Log Source       | Kali Linux                 |
| Log Collection         | Splunk Universal Forwarder |
| Investigation Language | Splunk SPL                 |
| Environment            | Isolated virtual lab       |

## Lab Architecture

The lab consists of a Splunk server receiving security logs from Windows and Linux virtual machines.

The collected events are analyzed using Splunk searches, dashboards, and alerts.

## Investigations

### Incident 01 – Windows Brute-Force Detection

Investigate multiple failed Windows logon attempts and identify suspicious authentication patterns.

### Incident 02 – Authentication Anomaly

Correlate failed and successful logon events to investigate suspicious authentication activity.

### Incident 03 – Suspicious PowerShell Activity

Investigate controlled PowerShell execution and identify relevant endpoint telemetry.

### Incident 04 – Linux Authentication Investigation

Analyze Linux authentication logs and investigate suspicious login activity.

## Skills Demonstrated

- SIEM monitoring
- Splunk Enterprise
- Log ingestion and analysis
- Windows Security Event Logs
- Linux authentication logs
- Splunk SPL
- Authentication investigation
- Event correlation
- Alert triage
- Incident documentation
- Basic incident response
- Git and GitHub documentation

## Safety

All security simulations are performed using authorized virtual machines in a controlled laboratory environment.

No real accounts, production systems, public targets, or destructive malware are used.

## Project Status

- [ ] Splunk configuration verification
- [ ] Windows log ingestion
- [ ] Linux log ingestion
- [ ] Incident 01 – Brute-force investigation
- [ ] Incident 02 – Authentication anomaly
- [ ] Incident 03 – PowerShell investigation
- [ ] Incident 04 – Linux authentication investigation
- [ ] Dashboard development
- [ ] Alert configuration
- [ ] Final incident report
- [ ] VMware environment validation
- [ ] Project screenshots
- [ ] GitHub documentation review
