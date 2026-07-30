# Enterprise SOC Lab using Splunk & Active Directory

> A Security Engineering portfolio project demonstrating centralized log collection, Windows security monitoring, detection engineering, incident investigation, and SOC dashboard development using Splunk Enterprise.

---

## Project Overview

This project demonstrates the design and implementation of a Security Operations Center (SOC) home lab using Splunk Enterprise, Active Directory, and Windows Event Logs.

The lab simulates a small enterprise environment where Windows systems generate security events that are forwarded to Splunk Enterprise using the Splunk Universal Forwarder. The collected logs are analyzed through custom SPL queries, detection rules, dashboards, and incident investigations.

This project showcases practical Security Engineering concepts including SIEM deployment, centralized logging, Windows monitoring, detection engineering, and incident response documentation.

---

## Project Objectives

- Build an enterprise-style SOC home lab
- Deploy Splunk Enterprise as a SIEM platform
- Configure centralized Windows Event Log collection
- Monitor authentication and Windows security events
- Develop custom SPL detection rules
- Build interactive SOC dashboards
- Investigate security incidents using Windows Event Logs
- Document detection logic and investigation workflows

---

# Architecture

```
                    +----------------------+
                    |   Windows 11 Client  |
                    +----------+-----------+
                               |
                               |
+-------------+       +---------v---------+
| Ubuntu      |       | Windows Server    |
| Server      |       | 2022 Domain Ctrl  |
+-------------+       +---------+---------+
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

Detailed documentation is available in:

```
architecture/
```

---

# Lab Environment

| Component | Technology |
|-----------|------------|
| SIEM | Splunk Enterprise 10.4 |
| Log Forwarder | Splunk Universal Forwarder |
| Domain Controller | Windows Server 2022 |
| Client Machine | Windows 11 |
| Linux Server | Ubuntu Server |
| Authentication | Active Directory |
| Virtualization | VirtualBox |

---

# Features

- Windows Event Log Collection
- Active Directory Integration
- Authentication Monitoring
- Security Event Visualization
- Detection Engineering
- Security Dashboard Development
- Windows Event Investigation
- Incident Documentation
- SPL Query Library
- Security Reporting

---

# Detection Rules

The project includes documented detection rules for:

- Brute Force Detection
- Successful Login After Multiple Failures
- New User Account Creation
- Privileged Group Membership Changes
- Password Reset Activity
- Account Lockout Detection

Each detection includes:

- Objective
- Windows Event IDs
- MITRE ATT&CK Mapping
- SPL Query
- Investigation Steps
- False Positives
- Recommended Response

Documentation:

```
detections/
```

---

# Security Dashboard

The Enterprise SOC Dashboard includes:

- Authentication Statistics
- Windows Event Distribution
- Investigation Timeline
- Top Hosts
- Event Types
- Recent Security Events

Dashboard documentation:

```
dashboards/
```

---

# Incident Investigations

Example SOC investigations included in this project:

- Brute Force Authentication Attempt
- New User Account Investigation
- Privileged Group Membership Investigation
- Password Reset Investigation
- Incident Investigation Template

Documentation:

```
investigations/
```

---

# SPL Query Library

The project includes reusable Splunk SPL queries for:

- Authentication Monitoring
- Dashboard Panels
- Detection Rules
- Windows Event Investigation

Documentation:

```
spl_queries/
```

---

# Configuration

Example Splunk configuration files included:

- inputs.conf
- outputs.conf
- server.conf

These files demonstrate how Windows Event Logs were collected and forwarded to Splunk Enterprise.

Documentation:

```
configs/
```

---

# Security Reports

Example SOC reporting documents include:

- Weekly Security Report
- Executive Summary
- Security Metrics

Documentation:

```
reports/
```

---

# Screenshots

## Enterprise SOC Dashboard

> Add dashboard-overview.png

---

## Authentication Statistics

> Add authentication-statistics.png

---

## Windows Event Distribution

> Add windows-event-distribution.png

---

## Investigation Timeline

> Add investigation-timeline.png

---

## Detection Alerts

> Add alerts screenshot

---

## Active Directory

> Add Active Directory screenshot

---

# Project Structure

```text
enterprise-soc-lab-splunk/
│
├── README.md
├── LICENSE
├── SECURITY.md
├── CONTRIBUTING.md
├── CHANGELOG.md
├── .gitignore
│
├── architecture/
│   └── architecture.md
│
├── configs/
│   ├── README.md
│   ├── inputs.conf
│   ├── outputs.conf
│   └── server.conf
│
├── dashboards/
│   ├── README.md
│   ├── dashboard-panels.md
│   ├── dashboard-setup.md
│   └── enterprise-soc-dashboard.md
│
├── detections/
│   ├── brute-force-detection.md
│   ├── successful-login-after-failures.md
│   ├── new-user-created.md
│   ├── privileged-group-change.md
│   ├── password-reset.md
│   └── account-lockout.md
│
├── investigations/
│   ├── brute-force-case.md
│   ├── new-user-investigation.md
│   ├── privilege-escalation.md
│   ├── password-reset-investigation.md
│   └── incident-template.md
│
├── lab/
│   └── environment.md
│
├── reports/
│   ├── executive-summary.md
│   ├── metrics.md
│   └── weekly-security-report.md
│
├── screenshots/
│
└── spl_queries/
    ├── authentication.md
    ├── dashboard-queries.md
    ├── detection-queries.md
    └── windows-event-queries.md
```

---

# Future Enhancements

- Sysmon Integration
- Linux Syslog Collection
- Microsoft Sysinternals
- Sigma Rule Integration
- MITRE ATT&CK Coverage Expansion
- Threat Hunting Playbooks
- Email Alerting
- Splunk Enterprise Security
- SOAR Integration
- Detection Rule Expansion

---

# Learning Outcomes

This project demonstrates practical experience with:

- SIEM Deployment
- Windows Event Logging
- Active Directory
- Splunk Enterprise
- Splunk Universal Forwarders
- Detection Engineering
- SPL (Search Processing Language)
- Security Monitoring
- Incident Investigation
- Dashboard Development
- Security Reporting
- SOC Documentation

---

# Author

**Anala Shasi Kumar**

Security Engineering Portfolio Project

LinkedIn: *[(Click)](https://www.linkedin.com/in/anala-shasi-kumar/)*

---

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.