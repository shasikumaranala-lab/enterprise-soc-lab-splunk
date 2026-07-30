# Dashboard Setup Guide

## Prerequisites

- Splunk Enterprise installed
- Windows Event Logs indexed
- Splunk Universal Forwarder configured

---

## Create Dashboard

1. Open Splunk Enterprise.
2. Navigate to **Dashboards**.
3. Select **Create New Dashboard**.
4. Name the dashboard **Enterprise SOC Dashboard**.

---

## Add Panels

Create the following panels:

- Authentication Statistics
- Windows Event Distribution
- Investigation Timeline
- Top Hosts
- Event Types
- Recent Security Events

---

## Visualization Types

| Panel | Visualization |
|--------|---------------|
| Authentication Statistics | Pie Chart |
| Windows Event Distribution | Bar Chart |
| Investigation Timeline | Line Chart |
| Top Hosts | Bar Chart |
| Event Types | Pie Chart |
| Recent Security Events | Table |

---

## Verification

After adding the panels:

- Verify events are indexed.
- Confirm SPL queries return results.
- Validate dashboard visualizations update correctly.