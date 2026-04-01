# Incident Validation

This document validates that detection rules created in Microsoft Sentinel successfully generated alerts and incidents based on simulated attack activity.

---

## Purpose

The goal of this phase is to confirm that detections are not only correctly written, but also function as expected in a real environment.

This ensures that:
- Alerts are triggered  
- Incidents are created  
- Relevant entities (users, IPs, systems) are captured  

---

## Validation Approach

Controlled activity was generated within the lab environment to simulate real-world attack behavior.

This included:
- Multiple failed login attempts  
- Failed logins followed by a successful login  
- Logins from unfamiliar or low-frequency IP addresses  
- Execution of PowerShell commands on the virtual machine  

Each activity was designed to trigger a corresponding detection rule.

---

## Detection Results

### 1. Brute Force Login Detection

- Alert Triggered: **Yes**  
- Incident Created: **Yes**  
- Entities Observed:
  - User account  
  - Source IP address  

**Observation:**  
Multiple failed login attempts within a short time window successfully triggered the detection rule and generated an incident in Microsoft Sentinel.

---

### 2. Failed Login Followed by Success

- Alert Triggered: **Yes**  
- Incident Created: **Yes**  
- Entities Observed:
  - User account  
  - Source IP address  

**Observation:**  
A sequence of failed login attempts followed by a successful login was detected and flagged as suspicious, indicating potential credential compromise behavior.

---

### 3. Suspicious IP Activity

- Alert Triggered: **Yes**  
- Incident Created: **Yes**  
- Entities Observed:
  - User account  
  - Source IP address  

**Observation:**  
Login activity from a low-frequency or unfamiliar IP address was identified and surfaced through the detection rule, providing additional context for investigation.

---

### 4. PowerShell / Endpoint Activity

- Alert Triggered: **Yes**  
- Incident Created: **Yes**  
- Entities Observed:
  - Host machine  
  - User account  

**Observation:**  
Execution of PowerShell commands on the virtual machine was successfully captured and detected, demonstrating endpoint-level visibility within the lab.

---

## Evidence

Screenshots of alerts and incidents can be found in the `/screenshots` directory, including:

- Detection results  
- Incident views  
- Workbook or log outputs  

---

## Summary

All detection rules were successfully validated through controlled testing.

This confirms that:
- Log ingestion is functioning correctly  
- Detection logic is effective  
- Microsoft Sentinel is properly generating alerts and incidents  

The lab demonstrates an end-to-end SOC workflow from activity → detection → incident creation.
