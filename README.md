🧠 Security Operations Triage Dashboard
✨ Overview

This project simulates a real-world Security Operations Centre (SOC) triage workflow using Microsoft Sentinel and KQL.

It demonstrates how security analysts detect, prioritise, and investigate suspicious activity across multiple data sources in an operational environment.

🔍 Focus Areas
🚨 Detecting suspicious authentication behaviour
🔐 Identifying brute force activity
👑 Monitoring privileged account usage
🌐 Correlating threat intelligence indicators
🔄 Investigating potential lateral movement
🎭 Scenario

An organisation begins experiencing unusual authentication activity across its environment.

⚠️ Indicators observed:
Multiple failed login attempts across several accounts
Successful logins from previously unseen IP addresses
Privileged account activity following authentication anomalies
Increased internal system-to-system connections
Matches with known malicious IP addresses

💡 This project simulates how a SOC analyst would triage and investigate this activity from initial detection through to response.

📊 Data Sources
🪟 SecurityEvent (Windows Security Logs)
☁️ SigninLogs (Azure AD authentication logs)
🧠 ThreatIntelligenceIndicator
🖥️ Syslog (optional)
🧩 Detection Strategy

This project uses a behaviour-based detection approach rather than relying only on known signatures.

🧠 Key detection logic:
Spikes in failed authentication attempts
Unusual login frequency or patterns
Abnormal privileged account activity
Suspicious internal network behaviour
Matches with external threat intelligence

✨ This reflects how modern SOC teams detect threats that bypass traditional controls.

🗺️ MITRE ATT&CK Mapping

This project aligns detection logic with real-world adversary behaviour using the MITRE ATT&CK framework.

🔗 Mappings
🚨 Brute Force Detection → Credential Access → T1110 (Brute Force)
🔓 Suspicious Successful Logons → Initial Access / Persistence → T1078 (Valid Accounts)
👑 Privileged Account Activity → Privilege Escalation → T1078 (Valid Accounts)
🌐 Threat Intelligence IP Match → Command & Control / Initial Access → Context-dependent
🔄 Lateral Movement → Lateral Movement → T1021 (Remote Services)
📝 Notes

These mappings support analyst reasoning, not definitive attribution.
They reflect how detections align with common attacker behaviours.

💻 Detection Queries

All detection logic is located in the /queries directory.

🔎 Example: Brute Force Detection
SecurityEvent  
| where EventID == 4625  
| summarize FailedAttempts = count() by Account, IpAddress, bin(TimeGenerated, 10m)  
| where FailedAttempts > 10  
| order by FailedAttempts desc  
🧠 SOC Triage Workflow

This project mirrors how real SOC teams operate:

🚨 Alerts are generated from analytics rules
🎯 Alerts are prioritised based on severity and context
🔗 Events are correlated across multiple data sources
✅ Suspicious behaviour is validated
📉 Impact is assessed
🛠️ Response actions are recommended
⚙️ Detection Rule Creation (Microsoft Sentinel)

The detections in this project are designed to be operationalised as scheduled analytics rules.

🪜 Steps

1. Create Analytics Rule
Navigate to the Analytics section in Sentinel

2. Define Rule Details

Name
Description
Severity
MITRE ATT&CK tactic

Example:
Brute Force Detection – Multiple Failed Logons
Severity: Medium
Tactic: Credential Access

3. Add KQL Query
Insert detection logic

4. Configure Scheduling

Run every: 5 minutes
Lookback: 15 minutes

5. Configure Alert Logic
Trigger when thresholds are met

6. Map Entities

Account → User
IP → IpAddress
Host → Computer

7. Apply MITRE Mapping
T1110 (Brute Force)

8. Configure Incidents
Enable automatic incident creation

9. Add Automation (Optional)

Notify analysts
Tag incidents
Trigger enrichment
📈 Dashboard Design (Workbook)

The triage dashboard provides a centralised operational view.

📊 Components
Failed login trends
Top attacking IP addresses
Suspicious successful logins
Privileged account activity
Threat intelligence matches
🎯 Purpose
Rapid anomaly detection
Faster prioritisation
Clear investigation context
🧪 Simulated Attack Flow
🚨 Attacker performs brute force attempts
🔓 Gains access to a valid account
🌍 Logs in from a new IP
👑 Accesses privileged functionality
🔄 Moves laterally across systems
🧠 Analyst Insights

Most attacks do not appear as obviously malicious.

Instead, they show up as small behavioural anomalies:

A login at an unusual time
A spike in failed authentication attempts
Access patterns that differ from normal behaviour

✨ Strong detection comes from context + pattern recognition, not just indicators.

🎯 Key Takeaways
Behaviour-based detection is essential
Correlation improves accuracy
Threat intelligence is strongest when combined with internal data
Detection is only step one — triage defines impact
📁 Repository Structure
security-ops-triage-dashboard/  
├── README.md  
├── queries/  
├── dashboards/  
├── sample-data/  
└── analyst-notes/  
⚠️ Disclaimer

This project uses simulated data and scenarios for educational purposes only.
