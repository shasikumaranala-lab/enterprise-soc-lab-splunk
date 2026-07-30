# Weekly Security Report

**Reporting Period:** YYYY-MM-DD to YYYY-MM-DD

---

# Executive Summary

This report summarizes security events collected by the Enterprise SOC Lab during the reporting period.

No critical incidents affecting the lab infrastructure were identified. Security monitoring successfully collected Windows event logs and generated alerts for configured detection rules.

---

# Environment Overview

| Component | Status |
|-----------|--------|
| Splunk Enterprise | Operational |
| Universal Forwarder | Operational |
| Windows Server 2022 | Online |
| Windows 11 | Online |
| Ubuntu Server | Online |

---

# Event Summary

| Category | Count |
|----------|------:|
| Total Events | XXX |
| Successful Logins | XXX |
| Failed Logins | XXX |
| Account Lockouts | XXX |
| Password Resets | XXX |
| New Users | XXX |

---

# Alerts Generated

| Alert | Severity | Count |
|-------|----------|------:|
| Brute Force Detection | High | X |
| Successful Login After Failures | High | X |
| New User Created | Medium | X |
| Password Reset | Medium | X |

---

# Top Event IDs

| Event ID | Description |
|----------|-------------|
|4624|Successful Login|
|4625|Failed Login|
|4720|User Created|
|4724|Password Reset|
|4740|Account Lockout|

---

# Recommendations

- Continue monitoring authentication events.
- Review account lockout policies.
- Enable Sysmon for endpoint visibility.
- Expand detection coverage.

---

# Conclusion

The monitoring infrastructure functioned as expected and successfully collected Windows security events for analysis.