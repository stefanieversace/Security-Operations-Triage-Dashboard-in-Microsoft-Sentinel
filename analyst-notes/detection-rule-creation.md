# Detection Rule Creation in Microsoft Sentinel

## Overview

Microsoft Sentinel analytics rules are used to run detection logic against ingested logs and generate alerts and incidents for SOC triage. Scheduled rules are one of the standard ways to create custom detections from KQL queries. :contentReference[oaicite:2]{index=2}

## Step-by-Step: Create a Scheduled Analytics Rule

### 1. Open the Analytics Rule Wizard
In Microsoft Sentinel, go to the **Analytics** area and create a new rule. You can create a rule from scratch or start from a template. Microsoft recommends using templates where possible, but custom rules can be created through the Analytics rule wizard when needed. :contentReference[oaicite:3]{index=3}

### 2. Define the Rule Details
Enter:
- Rule name
- Description
- Severity
- MITRE ATT&CK tactics

Microsoft documents that the rule name, description, severity, and MITRE ATT&CK tactics are defined at the start of the scheduled rule creation process, and these details are inherited by the alerts the rule generates. :contentReference[oaicite:4]{index=4}

Example:
- **Name:** Brute Force Detection – Multiple Failed Logons
- **Description:** Detects repeated failed Windows logon attempts from the same IP over a short time window.
- **Severity:** Medium
- **MITRE ATT&CK tactic:** Credential Access

### 3. Add the KQL Query
Paste the detection query into the rule logic section.

Example:

```kql
SecurityEvent
| where EventID == 4625
| summarize FailedAttempts = count() by Account, IpAddress, bin(TimeGenerated, 10m)
| where FailedAttempts > 10
| order by FailedAttempts desc
