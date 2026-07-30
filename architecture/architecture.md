# Enterprise SOC Lab Architecture

## Overview

The Enterprise SOC Lab is a simulated enterprise security environment designed to demonstrate centralized log collection, security monitoring, detection engineering, and incident investigation using Splunk Enterprise.

The lab replicates a basic Security Operations Center (SOC) workflow where Windows systems generate security events that are collected by the Splunk Universal Forwarder and forwarded to Splunk Enterprise for indexing and analysis.

Once the data is ingested, Splunk enables analysts to search events, build dashboards, create detection rules, investigate suspicious activities, and generate security reports.

This architecture provides practical experience with SIEM deployment, Windows event monitoring, and SOC operations.

---

# Architecture Diagram

```text
                    +----------------------+
                    |   Windows 11 Client  |
                    |  (Domain Endpoint)   |
                    +----------+-----------+
                               |
                               |
+----------------+     +-------v--------+
| Ubuntu Server  |     | Windows Server |
| (Linux Host)   |     | 2022 Domain    |
+----------------+     | Controller     |
                       +-------+--------+
                               |
                      Windows Event Logs
                               |
                               |
               Splunk Universal Forwarder
                               |
                     TCP Forwarding (9997)
                               |
                               v
                 +--------------------------+
                 |     Splunk Enterprise    |
                 |     Search Head & SIEM   |
                 +--------------------------+
                               |
          +---------+----------+----------+-----------+
          |         |                     |           |
          v         v                     v           v
      Event      Dashboards          Detection    Investigations
      Search                          Rules
```

---

# Architecture Components

## Splunk Enterprise

### Purpose

Splunk Enterprise acts as the centralized Security Information and Event Management (SIEM) platform within the lab.

It receives Windows event logs, indexes incoming data, and provides powerful search and visualization capabilities for security monitoring.

### Responsibilities

- Centralized log collection
- Event indexing
- SPL query execution
- Security dashboards
- Detection engineering
- Alert generation
- Incident investigation
- Security reporting

---

## Splunk Universal Forwarder

### Purpose

The Splunk Universal Forwarder is a lightweight agent installed on Windows Server.

Its primary responsibility is to collect Windows Event Logs and securely forward them to Splunk Enterprise.

### Responsibilities

- Monitor Windows Event Logs
- Forward logs to Splunk Enterprise
- Minimize resource usage
- Ensure continuous log delivery

---

## Windows Server 2022

### Purpose

Windows Server functions as the Active Directory Domain Controller for the lab environment.

It provides centralized authentication services while generating valuable Windows Security Events used for monitoring and detection.

### Responsibilities

- Active Directory Domain Services
- User Authentication
- Group Policy Management
- Account Management
- Security Event Generation

### Generated Event Types

- Successful Logins
- Failed Logins
- User Account Creation
- Password Changes
- Group Membership Changes
- Account Lockouts

---

## Windows 11 Client

### Purpose

The Windows 11 virtual machine represents a domain-joined enterprise endpoint.

It generates authentication events and user activity that are monitored by the SOC.

### Responsibilities

- User Authentication
- Endpoint Activity
- Windows Event Generation
- Client Security Monitoring

---

## Ubuntu Server

### Purpose

Ubuntu Server represents a Linux workload within the enterprise environment.

Although it is not currently forwarding logs, it provides a foundation for future Linux security monitoring.

### Planned Enhancements

- Syslog Collection
- Linux Authentication Logs
- SSH Monitoring
- Linux Threat Detection

---

# Data Flow

The following workflow illustrates how security events move through the monitoring pipeline.

```text
Windows Server

        │

Generate Windows Security Events

        │

        ▼

Splunk Universal Forwarder

        │

Collect & Forward Logs

        │

TCP 9997

        ▼

Splunk Enterprise

        │

Event Parsing

        │

Event Indexing

        │

Search Processing

        │

+----------------------------+
| SPL Queries                |
| Detection Rules            |
| Security Dashboards        |
| Incident Investigation     |
| Security Reports           |
+----------------------------+
```

---

# Network Architecture

| Component | Purpose |
|-----------|---------|
| Host Machine | Hosts Splunk Enterprise |
| Windows Server 2022 | Active Directory Domain Controller |
| Windows 11 Client | Domain-Joined Endpoint |
| Ubuntu Server | Linux Monitoring Target |

> Replace the placeholder IP addresses with your own lab IP addresses if you choose to document them.

---

# Log Collection

The following Windows Event Logs are collected and indexed in Splunk Enterprise.

| Log Source | Purpose |
|------------|---------|
| Windows Security | Authentication and security auditing |
| Windows System | Operating system events |
| Windows Application | Application events |
| Active Directory | User and domain activity |

Future versions of the lab will also include:

- Sysmon Events
- Linux Syslog
- PowerShell Operational Logs

---

# Detection Workflow

The Security Operations workflow implemented in this lab follows the standard SOC process.

```text
Windows Security Events

          │

          ▼

Splunk Universal Forwarder

          │

          ▼

Splunk Enterprise

          │

Event Indexing

          │

SPL Detection Rules

          │

Alert Generation

          │

SOC Dashboard

          │

Security Investigation

          │

Incident Documentation

          │

Security Reporting
```

---

# Security Monitoring Capabilities

The current implementation supports monitoring for the following security events.

| Capability | Windows Event IDs |
|------------|-------------------|
| Successful Login Monitoring | 4624 |
| Failed Login Detection | 4625 |
| User Account Creation | 4720 |
| Password Reset Monitoring | 4724 |
| Privileged Group Changes | 4728, 4732 |
| Account Lockout Detection | 4740 |

---

# Current Limitations

The current implementation focuses on Windows event monitoring.

The following capabilities are planned for future versions.

- Sysmon Event Collection
- Linux Security Monitoring
- Sigma Rule Integration
- MITRE ATT&CK Mapping
- Threat Hunting Dashboards
- Email Alerting
- Automated Response Workflows

---

# Future Enhancements

Planned improvements include:

- Integrate Sysmon for enhanced endpoint telemetry.
- Collect Linux authentication and system logs.
- Implement Sigma rule support.
- Expand MITRE ATT&CK technique coverage.
- Develop advanced threat hunting dashboards.
- Configure automated email notifications.
- Explore Splunk Enterprise Security (ES) capabilities.
- Add additional detection rules for lateral movement and privilege escalation.