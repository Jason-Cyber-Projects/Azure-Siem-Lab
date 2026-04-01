# Azure SOC Lab (Microsoft Sentinel)

## Overview
This project demonstrates the design and implementation of a cloud-based Security Operations Center (SOC) using Microsoft Azure and Microsoft Sentinel.

The environment simulates real-world security monitoring by ingesting authentication and endpoint logs, detecting suspicious activity, and validating alerts through controlled attack scenarios.

---

## What This Project Proves
- Ability to build and configure a SIEM (Microsoft Sentinel)
- Understanding of authentication and endpoint log analysis
- Experience writing detection logic using KQL
- Ability to validate alerts through simulated attack activity
- Exposure to incident response and automation workflows

---

## Environment Components
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
-  **Logins from different IP addresses for the same account** ( Geolocation detection)

---

## Validation Approach
Detection rules were tested by generating controlled activity within the environment, including repeated failed logins and endpoint actions, to ensure alerts were triggered and visible in Microsoft Sentinel.

---

## Automation
Basic automation was implemented to:
- Generate incidents in Microsoft Sentinel  
- Assign severity levels to alerts  
- Notify analysts of suspicious activity  
- Support initial triage workflows  

---

## Skills Demonstrated
- Azure infrastructure deployment  
- SIEM configuration and log ingestion  
- KQL query development  
- Detection engineering  
- Security event analysis  
- Incident response fundamentals  

---

## Project Structure
```plaintext
azure-soc-lab/
│
├── README.md
├── docs/
│   ├── detections.md
│   ├── incident-validation.md
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
│   ├── brute-force.kql
│   ├── failed-success.kql
```

---

## Notes
This project focuses on detection and response workflows rather than infrastructure complexity. The goal is to demonstrate practical SOC capabilities in a controlled cloud environment.

---

## Author
Jason P
