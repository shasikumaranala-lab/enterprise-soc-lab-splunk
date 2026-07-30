# Lab Environment

## Objective

The objective of this project is to build a practical Security Operations Center (SOC) lab capable of collecting, monitoring, and investigating security events using Splunk Enterprise.

---

## Virtual Machines

### Host Machine

- Operating System: Windows
- Role: Splunk Enterprise

---

### Windows Server 2022

Role:

- Active Directory Domain Controller
- Authentication Server
- Windows Event Log Source

---

### Windows 11

Role:

- Domain Client
- User Authentication
- Security Event Generation

---

### Ubuntu Server

Role:

- Linux Server
- Future Syslog Collection

---

## Software

- Splunk Enterprise
- Splunk Universal Forwarder
- VirtualBox
- Active Directory
- Windows Event Viewer

---

## Network

All virtual machines communicate through an internal VirtualBox network.

Windows systems forward security logs to Splunk Enterprise using TCP port 9997.

---

## Project Goals

- Centralized Logging
- Authentication Monitoring
- Detection Engineering
- Dashboard Development
- Incident Investigation

---

## Current Status

- Active Directory Configured
- Domain Controller Operational
- Splunk Enterprise Installed
- Universal Forwarder Configured
- Dashboard Developed
- Detection Rules Implemented