# Enterprise SOC Lab using Splunk & Active Directory

## Overview

This project demonstrates the design and implementation of a Security Operations Center (SOC) home lab using Splunk Enterprise, Active Directory, and Windows event monitoring.

The lab simulates an enterprise environment where Windows systems forward security logs to Splunk Enterprise for centralized monitoring, detection engineering, and incident investigation.

---

## Objectives

- Build an enterprise-style SOC home lab
- Centralize Windows Event Logs using Splunk Universal Forwarder
- Monitor authentication and system events
- Develop custom SPL detection rules
- Build interactive security dashboards
- Perform security investigations using Windows Event Logs

---

## Architecture

```
                    +----------------------+
                    |   Windows 11 Client  |
                    +----------+-----------+
                               |
                               |
                               |
+-------------+       +---------v---------+
| Ubuntu      |       | Windows Server    |
| Server      |       | 2022 Domain Ctrl  |
+-------------+       +---------+---------+
                                |
                                |
                     Splunk Universal Forwarder
                                |
                                |
                                v
                    +---------------------------+
                    |     Splunk Enterprise     |
                    |       Host Machine        |
                    +---------------------------+
```

---

## Lab Environment

| Component | Technology |
|-----------|------------|
| SIEM | Splunk Enterprise 10.4 |
| Log Forwarder | Splunk Universal Forwarder |
| Domain Controller | Windows Server 2022 |
| Client Machine | Windows 11 |
| Linux Server | Ubuntu Server |
| Virtualization | VirtualBox |
| Authentication | Active Directory |

---

## Features

- Windows Event Log Collection
- Active Directory Integration
- Authentication Monitoring
- Security Event Visualization
- Detection Engineering using SPL
- Interactive SOC Dashboard
- Security Event Investigation
- Windows Event Analysis

---

## Detection Rules

- Brute Force Detection
- Successful Login after Multiple Failures
- New User Detection
- Privileged Group Monitoring
- Password Reset Detection
- Account Lockout Detection

---

## Dashboard

The SOC dashboard includes:

- Authentication Overview
- Security Event Distribution
- Investigation Timeline
- Top Monitored Hosts
- Windows Event Categories
- Recent Security Activity

---

## Screenshots

### Enterprise SOC Dashboard

(Add dashboard screenshot here)

### Active Directory

(Add AD screenshot here)

### Detection Rules

(Add alerts screenshot here)

---

## Project Structure

```text
enterprise-soc-lab-splunk
├── architecture
├── dashboards
├── detections
├── investigations
├── configs
├── screenshots
├── spl_queries
└── lab
```

---

## Future Improvements

- Sysmon Integration
- Microsoft Sysinternals
- Sigma Rule Conversion
- MITRE ATT&CK Mapping
- Splunk Enterprise Security
- Threat Hunting Dashboards

---

## Author

Shasi Kumar Yadav

Security Engineering Portfolio Project