# Splunk Configuration Files

This directory contains the configuration files used to collect and forward Windows Event Logs from the Windows Server to Splunk Enterprise.

## Files

| File | Purpose |
|------|---------|
| inputs.conf | Defines Windows Event Log inputs |
| outputs.conf | Forwards events to Splunk Enterprise |
| server.conf | Server configuration (sanitized) |
| deploymentclient.conf | Optional deployment client configuration |

> **Note:** Sensitive information such as passwords, authentication tokens, and production IP addresses has been removed or replaced with placeholders.