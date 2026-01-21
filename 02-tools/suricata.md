# Suricata in a FOSS SOC

Suricata is an open-source Network Intrusion Detection and Prevention System (IDS/IPS).
In a SOC, it provides **network-level visibility** that host logs alone cannot capture.

This document explains **where Suricata fits**, **how it is used**, and **when it is worth deploying**.

---

## What Problem Suricata Solves

Host-based logs show:
- Authentication events
- Process activity
- Application errors

But they do not show:
- Network scans
- Exploit attempts
- Malicious payloads
- Command-and-control traffic

Suricata fills this visibility gap.

---

## Where Suricata Fits in SOC Architecture

Network Traffic  
→ Suricata  
→ JSON Events (eve.json)  
→ SOC Pipeline  
→ SIEM / Detection Engine  

Suricata acts as a **network sensor**, not a replacement for host monitoring.

---

## What Suricata Detects

- Port scans
- Exploit attempts
- Web attacks
- Malware communication
- Policy violations

Detection is based on:
- Signature rules
- Protocol analysis
- Behavioral indicators

---

## Deployment Models

### IDS Mode (Most Common)
- Passive monitoring
- No traffic blocking
- Low operational risk

Recommended for:
- Universities
- SMBs
- Research networks

---

### IPS Mode
- Inline traffic inspection
- Can block malicious traffic
- Higher operational risk

Recommended only for:
- Mature SOC teams
- Well-tested environments

---

## Log Output and SOC Integration

Suricata generates structured JSON logs:

- fast.log → human-readable alerts
- eve.json → structured events

For SOC usage:
- eve.json is forwarded to the log pipeline
- Events are indexed and correlated
- Alerts are enriched with host and threat context

---

## When Suricata Makes Sense

- Internet-facing services
- Public web applications
- Mail servers
- Research networks
- Compliance-driven environments

---

## When Suricata Is Overkill

- Very small internal networks
- Low traffic environments
- No dedicated monitoring staff

---

## Common Mistakes

- Deploying IPS without testing
- Monitoring wrong interfaces
- Ignoring rule tuning
- Treating Suricata alerts as final verdicts

Suricata alerts require **SOC context and correlation**.

---

## Key Takeaway

Suricata provides **network truth**.

When combined with host logs and proper correlation,
it significantly improves threat detection in a FOSS SOC.
