# Security Operations Triage Dashboard

## Overview

This project simulates a real-world Security Operations Centre (SOC) triage workflow using Microsoft Sentinel and KQL.

The goal is to demonstrate how security analysts prioritise, investigate, and respond to suspicious activity across multiple log sources.

This project focuses on:
- Detecting suspicious authentication behaviour
- Identifying brute force attacks
- Tracking privilege escalation
- Correlating threat intelligence indicators
- Investigating lateral movement activity

---

## Scenario

An organisation begins experiencing unusual authentication activity across its environment.

Indicators include:
- Multiple failed logins
- Suspicious successful logins from new locations
- Potential lateral movement between hosts
- Matches with known malicious IP addresses

This project simulates how a SOC analyst would triage and investigate this activity.

---

## Data Sources

- SecurityEvent (Windows logs)
- SigninLogs (Azure AD)
- ThreatIntelligenceIndicator
- Syslog (optional)

---

## Detection Strategy

The detection logic is built around behavioural anomalies rather than static signatures.

Key detection themes:
- Unusual login patterns
- High failure rates
- Privilege changes
- Threat intelligence matches
- Host-to-host movement

---

## Detection Queries

All queries are located in the `/queries` folder.

---

## Analyst Workflow

1. Identify alerts triggered by detection rules
2. Prioritise based on severity and context
3. Correlate events across data sources
4. Validate suspicious behaviour
5. Determine potential impact
6. Recommend response actions

---

## Analyst Insights

This project highlights a critical reality in modern security operations:

Most attacks do not appear as obvious malicious events.

Instead, they manifest as subtle deviations in normal behaviour:
- A login at an unusual time
- A spike in failed authentication attempts
- A user accessing systems they typically do not interact with

Effective detection relies on understanding patterns, not just indicators.

---

## Key Takeaways

- Behaviour-based detection is essential in modern SOC environments
- Correlation across logs significantly improves detection accuracy
- Threat intelligence is most effective when combined with internal telemetry
- Triage is about prioritisation, not just detection

---

## Disclaimer

This project uses simulated data and scenarios for educational purposes only.
