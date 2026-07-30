# Enterprise SOC Dashboard Documentation

## Overview

This directory contains the complete documentation for the **Enterprise SOC Dashboard** developed as part of the **Enterprise SOC Lab**.

The dashboard was built using **Splunk Enterprise** to provide centralized visibility into Windows security events collected from the lab environment. It serves as the primary interface for monitoring authentication activity, analyzing security events, validating detection rules, and supporting incident investigations.

The documentation in this directory explains the dashboard architecture, individual panels, deployment process, visualization design, and the SPL queries used to generate each panel.

---

# Purpose

The Enterprise SOC Dashboard is designed to simulate the monitoring capabilities of a Security Operations Center (SOC) by transforming Windows Event Logs into meaningful security visualizations.

The dashboard enables security analysts to:

- Monitor Windows authentication activity.
- Observe real-time security events.
- Analyze Windows Event Log trends.
- Identify suspicious behavior.
- Support incident investigations.
- Validate detection rules.
- Improve security visibility across monitored systems.

---

# Documentation Contents

This directory contains the following documentation:

| Document | Description |
|----------|-------------|
| **README.md** | Introduction to the dashboard documentation. |
| **enterprise-soc-dashboard.md** | Detailed overview of the Enterprise SOC Dashboard, architecture, objectives, and monitoring capabilities. |
| **dashboard-panels.md** | Documentation for each dashboard panel, including objectives, SPL queries, expected output, and security value. |
| **dashboard-setup.md** | Step-by-step deployment guide for recreating the dashboard within Splunk Enterprise. |

---

# Dashboard Features

The Enterprise SOC Dashboard provides centralized monitoring through the following capabilities:

- Windows Authentication Monitoring
- Windows Event Log Monitoring
- Security Event Visualization
- Event Timeline Analysis
- Host Activity Monitoring
- Windows Event Classification
- Real-Time Security Event Monitoring
- Detection Rule Validation
- Incident Investigation Support

---

# Dashboard Components

The dashboard consists of six primary panels that provide different perspectives of the collected Windows security events.

| Dashboard Panel | Purpose |
|-----------------|---------|
| Authentication Statistics | Displays successful and failed Windows authentication events. |
| Windows Event Distribution | Shows the distribution of collected Windows event logs. |
| Investigation Timeline | Visualizes security events over time to support investigations. |
| Top Hosts | Identifies systems generating the highest event volume. |
| Event Types | Displays the frequency of Windows Event IDs. |
| Recent Security Events | Displays the latest indexed security events for real-time monitoring. |

---

# Data Sources

The dashboard currently visualizes data collected from the following Windows log sources:

- Windows Security Logs
- Windows System Logs
- Windows Application Logs
- Active Directory Security Events

Future versions of the dashboard will include additional telemetry sources such as Sysmon, Linux Syslog, and PowerShell Operational Logs.

---

# Dashboard Screenshots

Screenshots demonstrating the completed dashboard are available in the **`screenshots/`** directory.

The screenshot collection includes:

- Enterprise SOC Dashboard Overview
- Authentication Statistics
- Windows Event Distribution
- Investigation Timeline
- Top Hosts
- Event Types
- Recent Security Events

These screenshots provide a visual reference for the dashboard layout and demonstrate how Windows security events are presented within Splunk Enterprise.

---

# Related Documentation

Additional documentation for the Enterprise SOC Lab is available throughout the repository.

```
architecture/
```

System architecture and log collection workflow.

```
configs/
```

Splunk configuration files used for log collection and forwarding.

```
spl_queries/
```

SPL queries used for dashboards, detections, and investigations.

```
detections/
```

Detection engineering documentation and alert logic.

```
investigations/
```

Incident response workflows and investigation playbooks.

```
reports/
```

Operational reports, executive summaries, and security metrics.

---

# Summary

The Enterprise SOC Dashboard is the central visualization component of the Enterprise SOC Lab. It consolidates Windows security telemetry into a unified monitoring interface, enabling analysts to monitor authentication activity, investigate security events, validate detection logic, and improve situational awareness through interactive dashboards powered by Splunk Enterprise.