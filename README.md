# 🧠 Security Operations Triage Dashboard

## Overview

This project simulates a real-world Security Operations Centre (SOC) triage workflow using Microsoft Sentinel and KQL.

It demonstrates how security analysts detect, prioritise, and investigate suspicious activity across multiple data sources in an operational environment.

### Focus Areas

- Detecting suspicious authentication behaviour  
- Identifying brute force activity  
- Monitoring privileged account usage  
- Correlating threat intelligence indicators  
- Investigating potential lateral movement  

---

## Scenario

An organisation begins experiencing unusual authentication activity across its environment.

### Indicators observed

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

This project uses a behaviour-based detection approach rather than relying only on known signatures.

Key detection logic includes:

- Spikes in failed authentication attempts  
- Unusual login frequency or patterns  
- Abnormal privileged account activity  
- Suspicious internal network behaviour  
- Matches with external threat intelligence  

---

## MITRE ATT&CK Mapping

- Brute Force Detection → Credential Access → T1110 (Brute Force)  
- Suspicious Successful Logons → Initial Access / Persistence → T1078 (Valid Accounts)  
- Privileged Account Activity → Privilege Escalation → T1078 (Valid Accounts)  
- Threat Intelligence IP Match → Command and Control / Initial Access → Context-dependent  
- Lateral Movement → Lateral Movement → T1021 (Remote Services)  

### Notes

These mappings support analyst reasoning and are not intended to represent definitive attribution.

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
