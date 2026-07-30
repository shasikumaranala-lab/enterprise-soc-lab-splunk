# Splunk Configuration Files

## Overview

This directory contains the Splunk configuration files used to configure log collection and data forwarding within the Enterprise SOC Lab.

These configuration files define how Windows Event Logs are collected from monitored systems, forwarded to Splunk Enterprise, and prepared for centralized security monitoring, detection engineering, and incident investigation.

The configurations included in this repository represent the core components of the log ingestion pipeline and demonstrate the setup required to integrate Windows systems with Splunk Enterprise in a lab environment.

---

# Configuration Workflow

The following workflow illustrates how Windows security events are collected and processed.

```text
Windows Event Logs
        │
        ▼
Splunk Universal Forwarder
        │
        ▼
Configuration Files
(inputs.conf / outputs.conf)
        │
        ▼
TCP Forwarding (Port 9997)
        │
        ▼
Splunk Enterprise
        │
        ▼
Indexing & Search
        │
        ├── Dashboards
        ├── Detection Rules
        ├── Alerts
        ├── Investigations
        └── Reports
```

---

# Configuration Files

| File | Description |
|------|-------------|
| **inputs.conf** | Defines the Windows Event Log sources that the Splunk Universal Forwarder monitors and collects. |
| **outputs.conf** | Configures the destination Splunk Enterprise server and manages secure event forwarding. |
| **server.conf** | Contains basic server configuration settings required by the Splunk instance. Sensitive values have been removed. |

---

# Purpose of Each Configuration

## inputs.conf

This file specifies which Windows Event Logs should be monitored by the Universal Forwarder.

Typical log sources include:

- Windows Security Logs
- Windows System Logs
- Windows Application Logs

These logs provide the telemetry required for authentication monitoring, detection engineering, and incident investigations.

---

## outputs.conf

This file defines where collected events are forwarded.

In this lab, the Universal Forwarder sends Windows Event Logs to Splunk Enterprise using TCP port **9997**, enabling centralized log collection and analysis.

---

## server.conf

This file contains general configuration settings for the Splunk instance, such as server identification and basic service parameters.

Only non-sensitive configuration examples are included in this repository.

---

# Security Considerations

To protect sensitive information, all configuration files included in this repository have been sanitized before publication.

The following information has been removed or replaced with placeholders:

- Server IP addresses
- Hostnames (where appropriate)
- Authentication credentials
- Passwords
- Security tokens
- Deployment information
- Environment-specific identifiers

---

# Educational Purpose

These configuration files are intended for educational and portfolio purposes only.

They demonstrate the fundamental configuration required to deploy a centralized Windows log collection pipeline using Splunk Enterprise and the Splunk Universal Forwarder.

For production environments, additional considerations such as encrypted communication, certificate management, deployment servers, indexer clustering, and role-based access control (RBAC) should be implemented.