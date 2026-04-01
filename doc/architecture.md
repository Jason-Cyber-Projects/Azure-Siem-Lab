# Architecture Overview

This document outlines the overall structure of the Azure SIEM lab and how data flows through the environment from activity to detection and incident creation.

---

## Environment Components

- **Azure Resource Group**  
  Contains all resources for the SOC lab environment. (Such as Virtual Machines and Log Analytic Workspaces)

- **Log Analytics Workspace**  
  Central location where logs are collected and stored.

- **Microsoft Sentinel**  
  SIEM platform used for detection, investigation, and incident management.

- **Windows Virtual Machine**  
  Simulated endpoint used to generate activity and security events.

- **Entra ID (Azure AD)**  
  Identity provider generating authentication and audit logs. Where Users and Groups are designed.

---

## Data Flow

User and system activity within the environment generates logs that are collected and analyzed through the following pipeline:

```
User Activity → Log Generation → Log Analytics Workspace → Microsoft Sentinel → Detection Rules → Incidents
```

### Flow Breakdown

1. **User Activity**
   - Login attempts (successful and failed)
   - Endpoint actions (PowerShell, system commands)

2. **Log Generation**
   - Entra ID produces sign-in and audit logs
   - Windows VM generates security event logs

3. **Log Ingestion**
   - Logs are sent to the Log Analytics Workspace

4. **Analysis (SIEM)**
   - Microsoft Sentinel queries logs using KQL
   - Detection rules analyze patterns and behavior

5. **Detection**
   - Suspicious activity triggers analytic rules
   - Alerts are generated based on defined conditions

6. **Incident Creation**
   - Alerts are grouped into incidents within Sentinel
   - Incidents provide context for investigation and response

---

## Identity and Access Structure

- Multiple users were created to simulate real-world activity
- Security groups were used to organize roles (e.g., users vs admin)
- Role-based access ensures proper visibility and control within the environment

---

## Purpose of Design

This architecture was designed to simulate a basic SOC workflow:
- Collect logs from multiple sources  
- Analyze activity centrally  
- Detect suspicious behavior  
- Generate actionable incidents  

The focus is on demonstrating detection and response capabilities rather than complex infrastructure design.
