# Enterprise SOC Dashboard

## Overview

The **Enterprise SOC Dashboard** is the primary monitoring interface of the Enterprise SOC Lab. It was developed using **Splunk Enterprise** to provide centralized visibility into Windows security events collected from the lab environment.

The dashboard consolidates security telemetry from multiple Windows event sources into a single interface, enabling security analysts to monitor authentication activity, analyze security events, investigate suspicious behavior, and identify trends across monitored systems.

By transforming raw Windows Event Logs into meaningful visualizations, the dashboard improves situational awareness and supports faster security investigations.

---

# Purpose

The primary objective of the dashboard is to simulate the monitoring capabilities of a Security Operations Center (SOC) by providing a centralized platform for security event analysis.

The dashboard enables analysts to:

- Monitor authentication activity in near real time.
- Analyze Windows security events across monitored systems.
- Detect abnormal authentication patterns.
- Identify hosts generating unusual event volumes.
- Correlate security events during investigations.
- Support detection engineering and threat analysis.

---

# Dashboard Architecture

The dashboard consumes indexed Windows Event Logs collected by the Splunk Universal Forwarder and processed by Splunk Enterprise.

```text
Windows Event Logs
        │
        ▼
Splunk Universal Forwarder
        │
        ▼
Splunk Enterprise
        │
Event Indexing
        │
        ▼
Enterprise SOC Dashboard
        │
        ├── Authentication Monitoring
        ├── Event Distribution
        ├── Timeline Analysis
        ├── Host Monitoring
        ├── Event Classification
        └── Recent Security Events
```

---

# Dashboard Objectives

The Enterprise SOC Dashboard was designed to achieve the following operational objectives:

- Provide centralized security monitoring.
- Visualize authentication activity.
- Monitor Windows event logs.
- Support security investigations.
- Identify abnormal event patterns.
- Improve security visibility.
- Validate detection rules.
- Reduce investigation time.

---

# Data Sources

The dashboard visualizes data collected from the following Windows log sources.

| Log Source | Purpose |
|------------|---------|
| Windows Security Logs | Authentication events, account management, privilege changes, and security auditing |
| Windows System Logs | Operating system events, services, drivers, and system health |
| Windows Application Logs | Application-level events, warnings, and errors |

Future versions of the dashboard will also support:

- Sysmon Operational Logs
- PowerShell Operational Logs
- Linux Syslog Events
- Endpoint Detection and Response (EDR) Telemetry

---

# Dashboard Panels

The dashboard consists of six primary panels that provide different perspectives of the collected security data.

| Panel | Description |
|--------|-------------|
| Authentication Statistics | Displays successful and failed Windows authentication events. |
| Windows Event Distribution | Shows the distribution of collected Windows event logs by source type. |
| Investigation Timeline | Visualizes event activity over time to assist with incident investigations. |
| Top Hosts | Identifies systems generating the highest number of indexed events. |
| Event Types | Displays the frequency of Windows Event IDs collected in the environment. |
| Recent Security Events | Displays the latest indexed security events for real-time monitoring. |

Detailed information about each panel, including SPL queries and visualization types, is available in:

```
dashboard-panels.md
```

---

# Security Monitoring Capabilities

The dashboard currently supports monitoring for the following Windows security events.

| Capability | Windows Event IDs |
|------------|-------------------|
| Successful Logon Monitoring | 4624 |
| Failed Logon Detection | 4625 |
| User Account Creation | 4720 |
| Password Reset Activity | 4724 |
| Privileged Group Membership Changes | 4728, 4732 |
| Account Lockout Detection | 4740 |

---

# Operational Benefits

The Enterprise SOC Dashboard provides several operational advantages for security monitoring.

### Centralized Visibility

Aggregates Windows security events from multiple systems into a single monitoring interface.

### Authentication Monitoring

Provides continuous visibility into successful and failed authentication attempts to help identify suspicious login activity.

### Faster Incident Investigation

Interactive visualizations enable analysts to quickly identify event spikes, investigate authentication failures, and correlate related events.

### Detection Validation

Supports validation of SPL detection rules by providing immediate visibility into collected security events.

### Security Reporting

Provides summarized event information that can be used to generate operational security reports and demonstrate monitoring coverage.

---

# Current Scope

The current implementation focuses on Windows-based security monitoring using Splunk Enterprise.

Implemented capabilities include:

- Windows Event Log Collection
- Active Directory Monitoring
- Authentication Monitoring
- Security Dashboard Development
- Detection Engineering
- SPL Query Development
- Incident Investigation
- Security Reporting

---

# Future Enhancements

The dashboard is designed to be expanded as the Enterprise SOC Lab evolves.

Planned enhancements include:

- Sysmon Integration
- Linux Log Collection
- PowerShell Operational Logging
- MITRE ATT&CK Technique Mapping
- Sigma Rule Integration
- Threat Hunting Dashboards
- Email Alerting
- Splunk Enterprise Security (ES)
- Additional Detection Rules
- Security Metrics Dashboard

---

# Related Documentation

The following documents provide additional information about the Enterprise SOC Lab.

```
architecture/
```

Overall system architecture and data flow.

```
configs/
```

Splunk configuration files used for log collection.

```
spl_queries/
```

SPL queries powering the dashboard and detection rules.

```
detections/
```

Detection engineering documentation.

```
investigations/
```

Incident investigation playbooks and case studies.

```
reports/
```

Security reports and operational metrics.

---

# Conclusion

The Enterprise SOC Dashboard serves as the central visualization layer of the Enterprise SOC Lab. It transforms raw Windows Event Logs into actionable security insights, enabling security analysts to monitor authentication activity, investigate security incidents, validate detection rules, and gain visibility into the overall security posture of the monitored environment.

This dashboard demonstrates practical SIEM implementation, centralized log analysis, and Security Operations Center (SOC) monitoring using Splunk Enterprise.