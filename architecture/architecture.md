# Enterprise SOC Lab Architecture

## Overview

The Enterprise SOC Lab simulates a small enterprise environment for centralized security monitoring using Splunk Enterprise.

Windows systems generate authentication and system events that are forwarded to Splunk Enterprise through the Splunk Universal Forwarder. Splunk indexes the events, enables custom SPL detections, and provides dashboards for monitoring and investigation.

---

## Architecture Components

### Splunk Enterprise

**Role**

- Centralized SIEM platform
- Event indexing
- Search and Reporting
- Detection Rules
- Dashboards
- Incident Investigation

---

### Splunk Universal Forwarder

**Role**

- Collect Windows Event Logs
- Forward logs to Splunk Enterprise
- Lightweight log collector

---

### Windows Server 2022

**Role**

- Active Directory Domain Controller
- User Authentication
- Group Policy
- Windows Security Events

---

### Windows 11 Client

**Role**

- Domain Joined Endpoint
- User Login Activity
- Authentication Events
- Client Security Events

---

### Ubuntu Server

**Role**

- Linux Monitoring Target
- Future Syslog Collection
- Linux Security Events

---

## Data Flow

```text
Windows Server
      │
      │ Windows Event Logs
      ▼
Splunk Universal Forwarder
      │
      │ TCP 9997
      ▼
Splunk Enterprise
      │
      ├── Event Indexing
      ├── SPL Queries
      ├── Detection Rules
      ├── Dashboards
      └── Incident Investigation
```

---

## Network Architecture

| Component | IP Address | Purpose |
|-----------|------------|---------|
| Host PC | YOUR_HOST_IP | Splunk Enterprise |
| Windows Server | YOUR_SERVER_IP | Domain Controller |
| Windows 11 | YOUR_CLIENT_IP | Domain Client |
| Ubuntu | YOUR_UBUNTU_IP | Linux Server |

---

## Log Collection

Current log sources include:

- Windows System Logs
- Windows Security Logs
- Windows Application Logs
- Active Directory Events

---

## Detection Workflow

```text
Windows Event

        ↓

Universal Forwarder

        ↓

Splunk Enterprise

        ↓

Indexing

        ↓

SPL Detection Rules

        ↓

Alerts

        ↓

SOC Dashboard

        ↓

Security Investigation
```

---

## Security Monitoring Capabilities

- Windows Authentication Monitoring
- Failed Login Detection
- Successful Login Detection
- User Account Monitoring
- Privileged Group Monitoring
- Password Reset Monitoring
- Account Lockout Monitoring

---

## Future Enhancements

- Sysmon Integration
- Linux Log Collection
- Sigma Rules
- MITRE ATT&CK Mapping
- Email Alerting
- Threat Hunting