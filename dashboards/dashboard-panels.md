# Dashboard Panels

## Overview

The Enterprise SOC Dashboard provides a centralized view of security events collected from the Windows environment. Each panel is designed to highlight a specific aspect of the security posture, enabling analysts to monitor authentication activity, identify suspicious behavior, investigate incidents, and understand event trends in real time.

The dashboard combines visualizations with Splunk Search Processing Language (SPL) queries to transform raw Windows Event Logs into actionable security insights.

---

# Dashboard Panel Summary

| Panel | Purpose | Visualization |
|--------|---------|---------------|
| Authentication Statistics | Monitor successful and failed authentication events | Pie Chart |
| Windows Event Distribution | Display the distribution of collected Windows event logs | Bar Chart |
| Investigation Timeline | Visualize security events over time | Line Chart |
| Top Hosts | Identify systems generating the highest event volume | Bar Chart |
| Event Types | Analyze the frequency of Windows Event IDs | Pie Chart |
| Recent Security Events | Display the latest collected security events | Table |

---

# Authentication Statistics

## Objective

This panel provides an overview of Windows authentication activity by displaying successful and failed login events.

Monitoring authentication trends helps analysts quickly identify abnormal login behavior, such as excessive failed authentication attempts that may indicate brute-force attacks or credential misuse.

### Windows Event IDs

| Event ID | Description |
|-----------|-------------|
| 4624 | Successful Logon |
| 4625 | Failed Logon |

### SPL Query

```spl
index=main (EventCode=4624 OR EventCode=4625)
| stats count by EventCode
```

### Expected Output

- Number of successful logins
- Number of failed logins

### Security Value

Provides a high-level overview of authentication activity and helps identify abnormal login patterns.

---

# Windows Event Distribution

## Objective

This panel displays the distribution of Windows event logs collected by Splunk.

It provides visibility into the different event sources being monitored and helps verify that expected log sources are continuously sending data.

### SPL Query

```spl
index=main
| stats count by sourcetype
```

### Expected Output

- Windows Security Logs
- Windows System Logs
- Windows Application Logs

### Security Value

Helps validate data ingestion and confirms that log collection is functioning correctly.

---

# Investigation Timeline

## Objective

This panel visualizes the volume of security events over time.

It enables analysts to correlate event spikes with suspicious activity, helping establish a timeline during incident investigations.

### SPL Query

```spl
index=main
| timechart span=1h count
```

### Expected Output

Hourly trend of collected security events.

### Security Value

Supports incident response by identifying unusual increases in event activity and establishing the sequence of events during an investigation.

---

# Top Hosts

## Objective

This panel identifies the systems generating the highest number of security events.

Monitoring event volume by host helps analysts quickly identify heavily active systems that may require additional investigation.

### SPL Query

```spl
index=main
| stats count by host
| sort -count
```

### Expected Output

A ranked list of hosts based on the number of indexed events.

### Security Value

Highlights systems producing unusually high event volumes, which may indicate configuration issues or suspicious activity.

---

# Event Types

## Objective

This panel summarizes Windows Event IDs collected within the environment.

It provides insight into the types of security events occurring across monitored systems and assists analysts in understanding overall security activity.

### SPL Query

```spl
index=main
| stats count by EventCode
```

### Expected Output

Frequency of Windows Event IDs such as:

- 4624 – Successful Logon
- 4625 – Failed Logon
- 4720 – User Account Created
- 4724 – Password Reset
- 4740 – Account Lockout

### Security Value

Provides a quick overview of the most common security events observed in the environment.

---

# Recent Security Events

## Objective

This panel displays the latest security events indexed by Splunk.

It enables analysts to monitor incoming events in near real time and quickly begin investigations when suspicious activity is detected.

### SPL Query

```spl
index=main
| table _time host source sourcetype
| sort -_time
```

### Expected Output

A chronological list of the most recently collected security events, including:

- Event Timestamp
- Host
- Source
- Source Type

### Security Value

Provides immediate visibility into current security activity and supports rapid incident investigation.

---

# Dashboard Benefits

The Enterprise SOC Dashboard provides several operational advantages for security monitoring:

- Centralized visibility into Windows security events
- Real-time monitoring of authentication activity
- Quick identification of abnormal event patterns
- Improved incident investigation through timeline visualization
- Validation of log collection and data ingestion
- Simplified monitoring through interactive visualizations

---

# Future Enhancements

The dashboard can be extended with additional panels to provide broader security visibility, including:

- Brute Force Detection
- Account Lockout Monitoring
- New User Account Creation
- Privileged Group Membership Changes
- Password Reset Activity
- Threat Summary Dashboard
- MITRE ATT&CK Technique Mapping
- Sysmon Event Monitoring
- Linux Security Monitoring
- Threat Hunting Dashboard