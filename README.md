# 🛡️ Security Operations Triage Dashboard

![Microsoft Sentinel](https://img.shields.io/badge/Microsoft%20Sentinel-SIEM-blue)
![KQL](https://img.shields.io/badge/KQL-Detection%20Engineering-5b5bd6)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE%20ATT%26CK-Mapped-red)
![Status](https://img.shields.io/badge/Status-Project%20Complete-brightgreen)
![Focus](https://img.shields.io/badge/Focus-SOC%20Triage%20%26%20Threat%20Detection-black)

A Microsoft Sentinel and KQL project simulating a real-world Security Operations Centre workflow for detecting, triaging, and investigating suspicious activity across enterprise log sources.

---

## Overview

This project demonstrates how a security analyst can use **Microsoft Sentinel**, **Kusto Query Language (KQL)**, and **MITRE ATT&CK mapping** to identify suspicious behaviour and prioritise incidents in a realistic SOC environment.

Rather than relying only on static indicators, the project uses a **behaviour-based detection approach** to surface patterns that may indicate account compromise, brute force activity, privilege misuse, or lateral movement.

---

## Objectives

- Detect suspicious authentication behaviour
- Identify brute force patterns
- Monitor privileged account activity
- Correlate threat intelligence indicators
- Investigate potential lateral movement
- Map detections to MITRE ATT&CK
- Show how detections can be operationalised in Microsoft Sentinel

---

## Tech Stack

- **Microsoft Sentinel**
- **Kusto Query Language (KQL)**
- **Windows Security Logs**
- **Azure AD Sign-in Logs**
- **Threat Intelligence Indicators**
- **MITRE ATT&CK Framework**

---

## Scenario

An organisation begins experiencing unusual authentication activity across its environment.

The simulated investigation includes:

- Multiple failed login attempts across user accounts
- Successful authentication from previously unseen IP addresses
- Privileged account activity following suspicious logons
- Increased host-to-host connections
- Threat intelligence matches against known malicious infrastructure

This project shows how an analyst could detect, triage, and investigate this activity from initial alerting through to impact assessment.

---

## Key Features

### Behaviour-Based Detection
The project focuses on identifying suspicious patterns in activity rather than depending entirely on known malicious signatures.

### SOC Triage Workflow
Detection logic is framed within a practical workflow: alert generation, prioritisation, correlation, validation, and response.

### MITRE ATT&CK Alignment
Queries are mapped to adversary tactics and techniques to connect technical findings to real-world attacker behaviour.

### Detection Engineering in Sentinel
The project demonstrates how KQL detections can be converted into scheduled analytics rules in Microsoft Sentinel.

---

## Repository Structure

```text
security-ops-triage-dashboard/
├── README.md
├── queries/
│   ├── brute_force_detection.kql
│   ├── suspicious_logons.kql
│   ├── privilege_activity.kql
│   ├── ti_ip_match.kql
│   └── lateral_movement.kql
├── dashboards/
│   └── workbook-notes.md
├── sample-data/
│   └── simulated-attack-flow.md
└── analyst-notes/
    ├── investigation-playbook.md
    └── sentinel-rule-creation.md
```

## Detection Queries

All detection logic is located in the queries/ directory.

Example: Brute Force Detection
SecurityEvent
| where EventID == 4625
| summarize FailedAttempts = count() by Account, IpAddress, bin(TimeGenerated, 10m)
| where FailedAttempts > 10
| order by FailedAttempts desc

This query identifies repeated failed logon attempts over a short time window, which may indicate password guessing or brute force behaviour.

## MITRE ATT&CK Mapping

Detection	Tactic	Technique
Brute Force Detection	Credential Access	T1110 - Brute Force
Suspicious Successful Logons	Initial Access / Persistence	T1078 - Valid Accounts
Privileged Account Activity	Privilege Escalation	T1078 - Valid Accounts
Threat Intelligence IP Match	Command and Control / Initial Access	Context-dependent
Lateral Movement	Lateral Movement	T1021 - Remote Services

### Notes

These mappings support analyst reasoning and are designed to show how detection logic aligns with common attacker behaviours. They are intended for operational context rather than definitive attribution.

## SOC Triage Workflow

1. Alert Generation

Analytics rules generate alerts when suspicious patterns match defined thresholds.

2. Prioritisation

Alerts are triaged based on severity, affected assets, account context, and supporting indicators.

3. Correlation

Relevant events are reviewed across multiple data sources to build investigation context.

4. Validation

Analysts assess whether the activity reflects expected behaviour, misconfiguration, or potential malicious action.

5. Impact Assessment

The scope of affected users, hosts, and systems is evaluated.

6. Response

Recommended actions may include account containment, IP blocking, escalation, or deeper incident response.

## Detection Rule Creation in Microsoft Sentinel

The detections in this project are designed to be operationalised as scheduled analytics rules in Microsoft Sentinel.

Typical configuration steps

1. Create a new scheduled analytics rule
2. Define rule metadata such as name, description, and severity
3. Insert the KQL detection query
4. Configure query frequency and lookback period
5. Define alert thresholds
6. Map entities such as account, IP address, and host
7. Apply MITRE ATT&CK tactics and techniques
8. Enable incident creation
9. Optionally attach automation or enrichment workflows

## Dashboard Design

The workbook concept for this project is designed to support fast operational triage.

### Suggested dashboard panels

- Failed login trends
- Top attacking IP addresses
- Suspicious successful logons
- Privileged account activity
- Threat intelligence matches
- Internal connection anomalies

This layout gives analysts a centralised view of suspicious activity and investigation context.

## Simulated Attack Flow

The project is built around a realistic multi-stage attack scenario:

- An attacker performs brute force attempts
- A valid account is compromised
- The attacker logs in from a new IP address
- Privileged functionality is accessed
- The attacker moves laterally across systems

## Analyst Insights

Most malicious behaviour does not appear as obviously malicious at first glance.

In many cases, the strongest indicators are subtle:

- an unusual login time
- a spike in authentication failures
- access from a new source IP
- abnormal privileged activity
- unexpected host-to-host movement

This is why modern detection engineering depends on pattern recognition, context, and cross-source correlation rather than isolated events alone.

## Key Takeaways

- Behaviour-based detection is critical in modern SOC environments
- Correlation across multiple data sources improves accuracy
- Threat intelligence is strongest when combined with internal telemetry
- Detection logic is more valuable when mapped to attacker behaviour
- Effective triage determines whether an alert becomes a meaningful investigation

## Why This Project Matters

This project is intended to demonstrate practical security analyst skills, including:

- detection engineering
- log analysis
- triage thinking
- adversary mapping
- operational use of Microsoft Sentinel
- investigation workflow design

It reflects the kind of thinking required in real-world SOC and threat detection roles, where technical signals must be translated into actionable security decisions.

## Future Improvements

- Add screenshots of Sentinel workbooks
- Add more advanced entity correlation
- Expand detections for impossible travel or anomalous sign-ins
- Include investigation notes for each alert
- Add sample incident summaries
- Create a companion case study PDF

## Disclaimer

This project uses simulated data and scenarios for educational and portfolio purposes only.
