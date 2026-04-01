# Detection Engineering

This document outlines the detection logic that was used in Microsoft Sentinel using KQL (Kusto Query Language). Each detection was designed to identify suspicious activity within the Azure and demonstrate practical analyst thinking through detection, validation, and response.

---

## 1. Brute Force Login Detection

### Purpose
Detect repeated failed login attempts that may indicate a brute force attack against a user account.

### Detection Logic
This detection looks for multiple failed authentication attempts against the same account within a short time window. Repeated failures can indicate password guessing, brute force activity, or unauthorized access attempts.

### KQL Query
```kql
SigninLogs
| where ResultType != 0
| summarize FailedAttempts = count() by UserPrincipalName, IPAddress, bin(TimeGenerated, 5m)
| where FailedAttempts >= 5
| sort by FailedAttempts desc
```

### Why It Matters
Brute force activity is a common initial access technique. Detecting it early helps identify accounts being targeted before access is successfully obtained.

### Analyst Response
- Review the targeted user account
- Check the originating IP address
- Determine whether the activity continued or led to a successful login
- Escalate or contain if compromise is suspected

---

## 2. Failed Login Followed by Successful Login

### Purpose
Detect a suspicious authentication sequence where repeated failed logins are followed by a successful login.

### Detection Logic
This pattern may indicate that a password was eventually guessed correctly or that an attacker successfully authenticated after multiple attempts. This is a higher-priority pattern than simple failed logins alone.

### KQL Query
```kql
SigninLogs
| where ResultType != 0
| summarize FailedCount = count(), LastFailedTime = max(TimeGenerated) by UserPrincipalName, IPAddress
| join kind=inner (
    SigninLogs
    | where ResultType == 0
    | project UserPrincipalName, SuccessIP = IPAddress, SuccessTime = TimeGenerated
) on UserPrincipalName
| where SuccessTime > LastFailedTime
| where SuccessTime <= LastFailedTime + 10m
| project UserPrincipalName, FailedIP = IPAddress, SuccessIP, FailedCount, LastFailedTime, SuccessTime
| sort by SuccessTime desc
```

### Why It Matters
A failed-then-success pattern can be a strong indicator of account compromise.

### Analyst Response
- Investigate the login timeline for the account
- Review the source IP and device details
- Check for post-login activity such as privilege changes or unusual access
- Reset credentials and enforce MFA if needed

---

## 3. Suspicious or Unfamiliar IP Detection

### Purpose
Detect sign-in activity originating from suspicious, unfamiliar, or externally sourced IP addresses.

### Detection Logic
This detection focuses on the source of authentication activity rather than only the success or failure result. In a SOC environment, source IP analysis is critical because unusual login locations or first-seen IP addresses can indicate unauthorized access attempts, password spraying, or compromised credentials.

### KQL Query
```kql
SigninLogs
| where ResultType == 0
| summarize LoginCount = count() by IPAddress, UserPrincipalName
| where LoginCount < 3
| sort by LoginCount asc
```

### Why It Matters
IP-based detection adds important context to authentication analysis. Even when a login succeeds, the originating IP may still indicate suspicious behavior that warrants investigation.

### Analyst Response
- Investigate whether the IP is expected or previously seen
- Compare the source IP to normal user behavior
- Review geolocation, frequency, and authentication outcome
- Correlate with failed logins, impossible travel, or abnormal sign-in timing

---

## 4. Suspicious PowerShell or Administrative Activity

### Purpose
Detect potentially suspicious command executions or administrative behavior on the Windows endpoint (The Virtual Machine)

### Detection Logic
PowerShell and administrative tools are commonly used by both administrators and attackers. This detection focuses on identifying activity that may indicate misuse of built-in tooling on the VM.

### KQL Query
```kql
SecurityEvent
| where EventID == 4688
| where Process contains "powershell"
| project TimeGenerated, Computer, Account, Process, CommandLine
| sort by TimeGenerated desc
```

### Why It Matters
Attackers frequently abuse native Windows tools after gaining access. Monitoring PowerShell or administrative process activity helps identify suspicious behavior that may not appear in authentication logs alone.

### Analyst Response
- Review the process or command activity in context
- Determine whether the behavior was expected or authorized
- Correlate with user logins and other alerts
- Investigate for lateral movement, discovery, or persistence behavior

---

## Detection Strategy Summary

The detections in this lab were built to monitor both authentication-based and endpoint-based activity. Together, they provide visibility into:

- Repeated failed authentication attempts
- Suspicious login sequences
- Risky or unfamiliar source IP activity
- Potential misuse of endpoint administrative tools

This layered detection approach better reflects real SOC monitoring than relying on a single alert type alone.
