# Enterprise SOC Dashboard Deployment Guide

## Overview

This document describes the deployment process for the **Enterprise SOC Dashboard** developed as part of the Enterprise SOC Lab.

The dashboard provides centralized visibility into Windows security events collected by Splunk Enterprise. It is designed to support security monitoring, authentication analysis, detection engineering, and incident investigations through interactive visualizations powered by Splunk Search Processing Language (SPL).

Following this guide allows the dashboard to be recreated in a new Splunk Enterprise environment using the queries documented within this repository.

---

# Prerequisites

Before deploying the dashboard, ensure the following components are correctly configured and operational.

| Requirement | Description |
|------------|-------------|
| Splunk Enterprise | Installed and accessible through the web interface |
| Splunk Universal Forwarder | Configured to forward Windows Event Logs |
| Windows Event Logs | Successfully indexed within Splunk |
| Active Directory | Configured (recommended) to generate authentication events |
| Search & Reporting App | Enabled for dashboard creation |
| SPL Queries | Available from the `spl_queries` directory |

---

# Deployment Workflow

The following workflow illustrates the dashboard deployment process.

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
Dashboard Creation
        │
        ▼
Panel Configuration
        │
        ▼
Visualization Selection
        │
        ▼
Dashboard Validation
```

---

# Dashboard Creation

## Step 1 — Access Splunk Enterprise

Log in to the Splunk Enterprise web interface using an account with permissions to create dashboards.

Navigate to:

```
Apps
   └── Search & Reporting
```

---

## Step 2 — Create a New Dashboard

Create a new dashboard using the following configuration.

| Property | Value |
|----------|-------|
| Dashboard Name | Enterprise SOC Dashboard |
| Visibility | Private or Shared |
| Layout | Grid |
| Theme | Default |

Once created, proceed to add dashboard panels.

---

# Dashboard Panels

Configure the following panels using the SPL queries provided in the `spl_queries/` directory.

| Panel | Purpose | Recommended Visualization |
|--------|---------|--------------------------|
| Authentication Statistics | Monitor successful and failed logins | Pie Chart |
| Windows Event Distribution | Display collected log sources | Bar Chart |
| Investigation Timeline | Visualize event activity over time | Line Chart |
| Top Hosts | Identify hosts generating the highest event volume | Bar Chart |
| Event Types | Display Windows Event ID distribution | Pie Chart |
| Recent Security Events | Display the latest indexed events | Table |

---

# Panel Configuration

For each dashboard panel:

1. Select **Add Panel**.
2. Choose **Search** as the data source.
3. Paste the corresponding SPL query.
4. Execute the search.
5. Select the recommended visualization.
6. Configure titles and descriptions.
7. Save the panel.
8. Repeat for all remaining panels.

---

# Dashboard Validation

After configuring all panels, verify that the dashboard is functioning correctly.

## Log Collection Validation

Confirm that:

- Windows Security Logs are being indexed.
- Windows System Logs are available.
- Windows Application Logs are available.
- Events are continuously received from monitored systems.

---

## Query Validation

Execute each SPL query individually to verify that:

- Search results are returned successfully.
- Expected Windows Event IDs are present.
- No syntax errors are reported.

---

## Visualization Validation

Verify that each panel displays the expected visualization.

| Panel | Expected Result |
|--------|-----------------|
| Authentication Statistics | Authentication event distribution |
| Windows Event Distribution | Log source distribution |
| Investigation Timeline | Event timeline |
| Top Hosts | Ranked host activity |
| Event Types | Event ID frequency |
| Recent Security Events | Latest indexed events |

---

# Functional Testing

Generate several Windows events to confirm the dashboard updates correctly.

Recommended test activities include:

- Successful user logon
- Failed login attempt
- User account creation
- Password reset
- Account lockout

After generating the events:

1. Refresh the dashboard.
2. Verify the events appear in the relevant panels.
3. Confirm event counts increase as expected.

---

# Expected Outcome

Upon successful deployment, the Enterprise SOC Dashboard should provide:

- Centralized visibility into Windows security events
- Real-time authentication monitoring
- Interactive event visualization
- Simplified security investigations
- Detection rule validation
- Improved situational awareness

---

# Troubleshooting

| Issue | Possible Cause | Resolution |
|------|----------------|-----------|
| No events displayed | Universal Forwarder not sending logs | Verify `inputs.conf` and `outputs.conf` |
| Empty panels | Incorrect SPL query | Validate query syntax |
| Missing Event IDs | Windows auditing not enabled | Enable required Windows audit policies |
| No timeline data | No indexed events | Confirm log forwarding and indexing |
| Host not visible | Forwarder offline | Verify Universal Forwarder service |

---

# Related Documentation

Additional documentation supporting the dashboard deployment is available within this repository.

```
architecture/
```

System architecture and data flow.

```
configs/
```

Splunk configuration files used for log collection.

```
spl_queries/
```

Complete library of SPL queries used throughout the project.

```
detections/
```

Detection rules and alert logic.

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

The Enterprise SOC Dashboard serves as the primary visualization layer of the Enterprise SOC Lab, transforming raw Windows Event Logs into actionable security insights.

By combining centralized log collection, SPL-based analytics, interactive dashboards, and documented detection logic, the dashboard provides a practical demonstration of how Security Operations Centers monitor, investigate, and respond to security events using Splunk Enterprise.