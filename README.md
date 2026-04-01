# Azure SIEM Lab (Microsoft Sentinel)

## Overview
This project simulates a small scale cloud-based Security Operations Center (SOC) using Microsoft Azure and Microsoft Sentinel.

The environment ingests identity and endpoint logs, applies detection logic using KQL, and generates alerts and incidents based on real-world attack scenarios such as brute-force attempts and suspicious endpoint activity.

---

## What This Project Demonstrates
- Ability to build, configure, and monitor a SIEM (Microsoft Sentinel)
- Ability to analyze authentication and endpoint logs
- Experience writing detection logic using KQL
- Ability to validate alerts through simulated attack activity
- Exposure to incident response and automation workflows

---

## Cloud Environment Components
- Azure Resource Group  
- Log Analytics Workspace  
- Microsoft Sentinel (SIEM)  
- Windows Virtual Machine (endpoint)  
- Entra ID users and groups  


---
## Data Sources
- Entra ID Sign-in Logs  
- Entra ID Audit Logs  
- Windows Security Event Logs (VM)  

---

## Detection Scenarios
- **Brute-force login attempts** (multiple failed logins)  
- **Failed login followed by success** (potential credential compromise)  
- **Suspicious endpoint activity** (PowerShell/admin behavior)
-  **Sign-ins from different IP addresses for the same account** (unusual access patterns)

---

## Validation Approach
Detection rules were tested then validated by controlled activity within the environment, including repeated failed logins and endpoint actions, to ensure alerts were triggered and visible in Microsoft Sentinel.

---

## Automation
Automation was implemented to:
- Generate incidents in Microsoft Sentinel  
- Assign severity levels to alerts  
- Notify analysts of suspicious activity  
- Support initial triage workflows  

---

## Skills Demonstrated
- Detection engineering using KQL
- Security event analysis
- SIEM configuration and log ingestion
- Azure infrastructure deployment
- Incident response fundamentals

---

## Project Structure
```plaintext
azure-soc-lab/
│
├── README.md
├── docs/
│   ├── detections.md
│   ├── automation.md
│   ├── architecture.md
│
├── screenshots/
│   ├── detection.png
│   ├── incident.png
│   ├── workbook.png
│   ├── automation.png
│
├── queries/
│   ├── Excessive-Failed-Logins.kql
│   ├── Failed-Logins-Then-Successful-Login.kql
│   ├── Different-IP-Sign-In.kql
│   ├── Endpoint-Powershell-Alert.kql
```
---
## Key Takeaways

- Detections must be validated with real activity, not assumptions
- Excessive logging without tuning leads to alert fatigue
- Correlating identity and endpoint logs improves visibility
- Effective SOC workflows require both detection and response
---

## Notes
This project focuses on detection and response workflows and to demonstrate practical SOC capabilities in a controlled cloud environment rather than to prove knowledge of Azure infrastructure (even though a understanding of said infrastructure was needed to get this to work)

---

## Author
Jason P
