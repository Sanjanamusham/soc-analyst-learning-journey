# SIEM and the SOC Analyst Relationship

*Notes from LetsDefend: SOC Fundamentals. Written in my own words while learning.*

## What is a SIEM?

SIEM stands for Security Information and Event Management. It's a tool that collects logs from all over a company (servers, firewalls, laptops, proxies) and looks through them for suspicious activity. When something matches a rule, it creates an **alert**.

The way I picture it: the SIEM is the alarm system, and the SOC analyst is the person who checks why the alarm went off.

## Popular SIEM tools

- Splunk
- IBM QRadar
- Microsoft Sentinel
- ArcSight
- FortiSIEM
- Wazuh (open source, good for home labs)

The interfaces differ, but the idea is the same: collect logs, apply rules, raise alerts.

## Who does what?

One thing that surprised me: SOC analysts usually **don't build the SIEM rules**. Other teams handle configuration and rule correlation. The analyst's main job starts once an alert shows up.

| Task | Who usually does it |
|------|---------------------|
| Set up the SIEM and log sources | Engineers / SIEM admins |
| Write and tune detection rules | Detection engineers / senior staff |
| Review and investigate alerts | SOC analysts |

## What an analyst does with an alert

The core question is always: **is this a real threat or a false positive?**

To answer it, the analyst doesn't rely on the SIEM alone. They check other tools too:

- **EDR:** What happened on the actual endpoint?
- **Log management:** What do the raw logs say?
- **Threat intelligence feeds:** Is this IP, URL, or file hash known to be malicious?

## The alert workflow

In the LetsDefend Monitoring page, the flow looks like this:

1. **Main Channel:** New alerts land here. It's a shared queue, so the whole team sees it.
2. **Take Ownership:** I pick an alert and take ownership. It moves to the **Investigation Channel**, so teammates know I'm on it and don't duplicate work.
3. **Investigate:** I open the alert details and collect what I need: hostname, IP address, URL, file hash, and what action the device took (for example, blocked or allowed).
4. **Decide:** Real threat or false positive?
5. **Close:** The alert moves to **Closed Alerts**.
