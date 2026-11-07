# SOC Types and Roles

*Notes from LetsDefend: SOC Fundamentals. Written in my own words while learning.*

## What is a SOC?

A Security Operations Center (SOC) is the team (and the place) that keeps an eye on a company's systems 24/7. They watch for suspicious activity, figure out if it's a real attack, and respond before it turns into a bigger problem.

The way I think about it: if the company is a building, the SOC is the security room with all the camera feeds.

## Types of SOC models

| Model | What it means | Where it fits |
|-------|---------------|---------------|
| In-house SOC | The company builds and runs its own SOC with its own people and tools | Large companies with a big budget and strict data control needs |
| Virtual SOC | A remote team monitors security, with no dedicated physical SOC room | Smaller companies, or teams that work remotely |
| Co-managed SOC | The company's own team and an outside security provider share the work | Companies that have some security staff but need extra coverage |
| Command SOC | A higher-level SOC that coordinates other SOCs and sets overall strategy | Very large or global organizations with several SOCs |

**My takeaway:** There's no single "best" model. It mostly comes down to budget, company size, and how much control the company wants over its own data.

## Roles in a SOC

Different people handle different parts of the job:

- **Tier 1 analyst:** Watches the alerts coming in and does the first check. Is it a real threat or a false alarm? Escalates if it looks serious.
- **Tier 2 analyst:** Takes escalated cases and investigates deeper, using logs and other tools to understand what actually happened.
- **Tier 3 analyst / threat hunter:** Handles the most complex incidents and goes looking for threats that the automatic alerts didn't catch.
- **Incident responder:** Contains the attack and helps fix it (this is where remediation happens).
- **SOC manager:** Runs the team, handles reporting, schedules, and makes sure processes are followed.

Exact job titles change from company to company, but the idea is the same: alerts get checked first, and harder cases move up.

## Words I had to look up

- **Alert:** A warning created when something looks suspicious.
- **False positive:** An alert that looked bad but turned out to be harmless.
- **Escalation:** Passing a case to someone more experienced.
- **Remediation:** Fixing the problem after it's found, for example removing malware or patching a vulnerability.

## Why this matters to me

I want to start as a Tier 1 analyst, so the main skills I need to build are:

- Reading alerts and logs carefully
- Telling real threats from false positives
- Writing clear investigation notes

## Questions I still have

- How do small companies decide between a virtual SOC and a co-managed one?
- What does a typical day look like for a Tier 1 analyst?

---
*Next note: SIEM and the analyst relationship*
