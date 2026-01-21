# Brute-Force Login Detection in a FOSS SOC

Brute-force attacks are one of the most common and effective attack techniques.
They target services such as SSH, mail, VPN, and web applications.

This document explains how a SOC detects brute-force activity
using logs, correlation logic, and contextual analysis.

---

## Attack Overview

A brute-force attack involves:
- Multiple authentication attempts
- Short time window
- Same source IP or user
- Repeated failures

If undetected, brute-force attacks lead to:
- Account compromise
- Lateral movement
- Privilege escalation

---

## Log Sources Used

Typical log sources include:
- auth.log (SSH)
- Mail authentication logs
- Web application login logs
- VPN authentication logs

Each log must contain at least:
- Timestamp
- Source IP
- Username (if available)
- Authentication result (success/failure)

---

## Detection Logic (Conceptual)

The detection logic is based on **behavior**, not signatures.

### Basic Rule

Trigger an alert when:
- Failed login attempts ≥ 5
- Time window ≤ 2 minutes
- Same source IP OR same username

---

## Example Detection Flow

1. Logs are ingested into the SOC pipeline
2. Authentication failures are extracted
3. Events are grouped by source IP or user
4. Count of failures is calculated
5. Threshold breach generates an alert

---

## Reducing False Positives

Brute-force detection must be tuned carefully.

### Common False Positives
- Users forgetting passwords
- Automated scripts
- Monitoring systems

### Mitigation Techniques
- Ignore known internal IPs
- Whitelist trusted services
- Increase threshold for internal users
- Correlate with successful login

---

## Contextual Enrichment

Alerts become more valuable when enriched with:
- Geo-location of IP
- Previous activity of IP
- Whether login eventually succeeded
- Target service importance

Context turns alerts into investigations.

---

## SOC Response Actions

Typical response steps:
1. Validate alert context
2. Check if login succeeded
3. Block source IP (if external)
4. Reset affected credentials
5. Investigate lateral movement

---

## Why This Detection Matters

- High signal-to-noise ratio
- Early attack detection
- Prevents credential compromise
- Easy to explain to stakeholders

Brute-force detection is a **baseline requirement**
for any serious SOC.

---

## Key Takeaway

Effective brute-force detection relies on:
- Clean log ingestion
- Proper correlation
- Sensible thresholds
- Context-aware response

Detection is not about alerts —
it is about **actionable security outcomes**.
