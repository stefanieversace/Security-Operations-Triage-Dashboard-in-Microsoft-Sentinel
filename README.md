# Security Operations Triage Dashboard

## Overview

This project simulates a real-world Security Operations Centre (SOC) triage workflow using Microsoft Sentinel and KQL.

It demonstrates how security analysts detect, prioritise, and investigate suspicious activity across multiple data sources in an operational environment.

The project focuses on:

- Detecting suspicious authentication behaviour
- Identifying brute force activity
- Monitoring privileged account usage
- Correlating threat intelligence indicators
- Investigating potential lateral movement

---

## Scenario

An organisation begins experiencing unusual authentication activity across its environment.

Observed indicators include:

- Multiple failed login attempts across several accounts
- Successful logins from previously unseen IP addresses
- Privileged account activity following authentication anomalies
- Increased internal system-to-system connections
- Matches with known malicious IP addresses

This project simulates how a SOC analyst would triage and investigate this activity from initial detection through to response.

---

## Data Sources

- SecurityEvent (Windows Security Logs)
- SigninLogs (Azure AD authentication logs)
- ThreatIntelligenceIndicator
- Syslog (optional)

---

## Detection Strategy

The detection approach is behaviour-based rather than signature-based.

Instead of relying solely on known indicators, the queries focus on identifying anomalies such as:

- Spikes in failed authentication attempts
- Unusual login frequency or patterns
- Abnormal privileged account activity
- Suspicious internal network behaviour
- Matches with external threat intelligence

This reflects how modern SOC teams detect threats that bypass traditional controls.

---

## MITRE ATT&CK Mapping

This project maps detection logic to the MITRE ATT&CK framework to align technical activity with known adversary behaviours.

| Detection | Tactic | Technique | Description |
|----------|--------|----------|------------|
| Brute Force Detection | Credential Access | T1110 Brute Force | Multiple failed login attempts may indicate password guessing or credential stuffing |
| Suspicious Successful Logons | Initial Access / Persistence | T1078 Valid Accounts | Successful authentication using potentially compromised credentials |
| Privileged Account Activity | Privilege Escalation | T1078 Valid Accounts | Elevated access following suspicious login behaviour |
| Threat Intelligence IP Match | Command and Control / Initial Access | T1071 Application Layer Protocol (context-dependent) | Activity involving known malicious infrastructure |
| Lateral Movement | Lateral Movement | T1021 Remote Services | Repeated internal logons across hosts indicating system traversal |

### ATT&CK Mapping Notes

These mappings are used to support analyst reasoning and investigation context.

They are not intended to represent definitive attribution, but rather to align detection logic with common adversary techniques observed in real-world environments.

---

## Detection Queries

All detection logic is located in the `/queries` directory.

### Example: Brute Force Detection

```kql
SecurityEvent
| where EventID == 4625
| summarize FailedAttempts = count() by Account, IpAddress, bin(TimeGenerated, 10m)
| where FailedAttempts > 10
| order by FailedAttempts desc
SOC Triage Workflow

This project reflects a realistic SOC triage process:

Alerts are generated from analytics rules
Alerts are prioritised based on severity and context
Events are correlated across multiple data sources
Suspicious behaviour is validated
Impact is assessed
Response actions are recommended
Detection Rule Creation in Microsoft Sentinel

The detections in this project are designed to be operationalised as scheduled analytics rules in Microsoft Sentinel.

Step 1: Create Analytics Rule

Navigate to the Analytics section in Sentinel and create a new scheduled rule.

Step 2: Define Rule Details
Name
Description
Severity
MITRE ATT&CK tactic

Example:

Name: Brute Force Detection – Multiple Failed Logons
Severity: Medium
Tactic: Credential Access
Step 3: Add KQL Query

Insert the detection query into the rule logic.

Step 4: Configure Scheduling
Run query every: 5 minutes
Lookback period: 15 minutes
Step 5: Configure Alert Logic

Trigger an alert when query results exceed defined thresholds.

Step 6: Map Entities
Account → User
IpAddress → IP
Computer → Host
Step 7: Apply MITRE ATT&CK Mapping

Example:

Tactic: Credential Access
Technique: T1110 Brute Force
Step 8: Configure Incident Settings

Enable automatic incident creation for triggered alerts.

Step 9: Add Automated Response (Optional)
Notify analysts
Tag incidents
Trigger enrichment workflows
Dashboard Design (Microsoft Sentinel Workbook)

The triage dashboard provides a centralised view of security activity.

Components:
Failed login trends (time series)
Top attacking IP addresses
Suspicious successful logins
Privileged account activity
Threat intelligence matches
Purpose:
Enable rapid anomaly detection
Support prioritisation of incidents
Provide context for investigations
Simulated Attack Flow

The project models a realistic attack sequence:

Attacker performs brute force attempts
Gains access to a valid account
Logs in from a new IP address
Accesses privileged functionality
Moves laterally across systems
Analyst Insights

This project highlights a key reality in modern cybersecurity:

Most malicious activity does not appear as obviously malicious.

Instead, attacks present as small deviations in behaviour:

A login at an unusual time
A spike in failed authentication attempts
Access patterns that differ from normal user behaviour

Effective detection relies on identifying patterns and context, not just known indicators.


Key Takeaways

Behaviour-based detection is critical in modern SOC environments
Correlation across multiple data sources improves detection accuracy
Threat intelligence is most effective when combined with internal telemetry
Detection is only the first step — triage and investigation determine impact

Repository Structure
security-ops-triage-dashboard/
│
├── README.md
├── queries/
├── dashboards/
├── sample-data/
└── analyst-notes/

Disclaimer

This project uses simulated data and scenarios for educational purposes only.


