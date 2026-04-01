# Automation and Response

This document outlines the basic automation and response workflow implemented in Microsoft Sentinel.

---

## Purpose

The purpose of automation in this lab is to demonstrate the ability to respond to security events, not just detect them.

This includes:
- Triggering alerts based on detection rules  
- Creating incidents automatically  
- Assigning severity levels  
- Supporting initial triage  

---

## Automation Workflow

### Trigger Condition

Automation is triggered when a detection rule identifies suspicious activity, such as:

- Multiple failed login attempts  
- Failed login followed by a successful login  
- Login from a suspicious or unfamiliar IP address  
- PowerShell or administrative activity on the endpoint  

---

### What It Does

When a detection is triggered:

- An **alert** is generated in Microsoft Sentinel  
- Alerts are grouped into an **incident**  
- The incident is assigned a **severity level**  
- Relevant entities are attached:
  - User account  
  - IP address  
  - Host machine  

---

### Severity Assignment

Severity levels were used to prioritize alerts:

- **Low** → Unusual but not clearly malicious  
- **Medium** → Suspicious activity requiring investigation  
- **High** → Strong indicator of compromise  

This helps guide analyst response and triage priority.

---

### Why This Matters

Automation improves SOC efficiency by:

- Reducing manual effort  
- Standardizing incident creation  
- Ensuring consistent alert handling  
- Enabling faster response times  

Even basic automation ensures that important events are not missed.

---

## Analyst Response Workflow

Once an incident is created:

1. Review alert details and associated logs  
2. Identify affected user, IP, or system  
3. Analyze login behavior or process activity  
4. Determine whether the activity is expected or suspicious  
5. Take action:
   - Reset credentials  
   - Investigate IP address  
   - Escalate if necessary  

---

## Future Improvements

This lab focuses on foundational automation. In a production SOC, automation could be expanded to include:

- Playbooks using Azure Logic Apps  
- Automated email or Teams notifications  
- Automatic account lockout or containment actions  
- Integration with ticketing systems  

---

## Summary

This automation workflow demonstrates the transition from detection to response. Alerts are automatically converted into actionable incidents, allowing for structured investigation and efficient SOC operations.
