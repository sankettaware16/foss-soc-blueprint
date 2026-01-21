# File Integrity Monitoring in a FOSS SOC

File Integrity Monitoring (FIM) is critical for detecting unauthorized
changes to systems, binaries, and configuration files.

A robust FIM design combines real-time detection with periodic verification.

---

## Why Hybrid FIM Is Needed

Single-method FIM has limitations:

- Real-time monitoring may miss context
- Scheduled scans may miss immediate attacks

A hybrid approach provides complete coverage.

---

## Components of Hybrid FIM

### Real-Time Monitoring
- Detects file changes instantly
- Useful for active attacks

### Scheduled Auditing
- Verifies cryptographic integrity
- Detects stealthy or delayed changes

---

## Architecture Overview

Critical Directories  
→ Real-Time Watcher  
→ JSON Logs  
→ SOC Pipeline  

Scheduled Auditor  
→ Integrity Verification  
→ JSON Logs  
→ SOC Pipeline  

---

## Real-Time Monitoring (Inotify)

Responsibilities:
- Watch critical directories
- Detect create, modify, delete, move events
- Generate structured logs

Strengths:
- Immediate visibility
- Low latency

Limitations:
- Cannot verify historical integrity
- May generate noise if not tuned

---

## Scheduled Auditing (Tripwire)

Responsibilities:
- Maintain cryptographic baseline
- Detect unauthorized modifications
- Periodically re-validate integrity

Strengths:
- High accuracy
- Cryptographic assurance

Limitations:
- Not real-time
- Requires tuning to reduce noise

---

## Noise Reduction Strategy

Effective FIM requires:
- Excluding dynamic directories
- Ignoring temporary files
- Focusing on high-value paths

Examples of critical paths:
- /etc
- /usr/local/sbin
- Application directories

---

## SOC Value of Hybrid FIM

- Detects persistence mechanisms
- Identifies insider activity
- Supports compliance and audits
- Provides forensic evidence

---

## Key Takeaway

FIM should not be treated as a checkbox feature.

A hybrid design ensures both speed and accuracy,
making FIM a reliable detection source in a SOC.
