# Log Ingestion Pipeline in a FOSS SOC

A reliable log ingestion pipeline is the foundation of any Security Operations Center (SOC).
If logs are delayed, dropped, or malformed, detections and investigations fail.

This document explains a **scalable and production-proven log ingestion pipeline**
using open-source components.

---

## Why a Pipeline Is Needed

Organizations generate logs from multiple sources:
- Linux servers
- Mail servers
- Web servers
- Firewalls
- Network devices

Sending logs directly to a SIEM often leads to:
- Performance bottlenecks
- Data loss during spikes
- Tight coupling between systems

A pipeline decouples log generation from log analysis.

---

## High-Level Flow

Log Sources  
→ Log Collector  
→ Message Queue  
→ Log Processor  
→ Storage & Search  

Each stage has a clear responsibility.

---

## Stage 1: Log Sources

Examples:
- auth.log / syslog
- Mail logs (Postfix, Roundcube)
- Web logs (Apache, NGINX)
- Firewall logs

Logs are generated locally on systems and **should never talk directly to the SIEM**.

---

## Stage 2: Log Collector (rsyslog)

rsyslog acts as a **single point of contact** for all log sources.

Responsibilities:
- Collect logs from multiple services
- Tag logs by source or type
- Forward logs reliably

Why rsyslog:
- Lightweight
- Preinstalled on most Linux systems
- Supports multiple outputs

---

## Stage 3: Message Queue (Kafka)

Kafka sits between log collection and processing.

Responsibilities:
- Buffer logs during traffic spikes
- Prevent data loss if downstream systems fail
- Decouple producers and consumers

When Kafka is useful:
- Medium to large environments
- Bursty log traffic
- Multiple consumers (SIEM, ML, archive)

When Kafka is overkill:
- Very small setups
- Low log volume
- Single-server SOC

---

## Stage 4: Log Processing (Logstash or Custom Parser)

At this stage, raw logs are:
- Parsed
- Normalized
- Enriched

Responsibilities:
- Convert raw text to structured JSON
- Extract fields (user, IP, action)
- Add metadata (host, source, geo)

This stage prepares logs for detection and analysis.

---

## Stage 5: Storage & Search (Elasticsearch)

Elasticsearch is the **central data store**.

Responsibilities:
- Index structured logs
- Enable fast search
- Support detection queries
- Retain historical data

Indexing strategy and retention policies are critical for performance and cost control.

---

## Why This Architecture Works

- Fault tolerant
- Scales horizontally
- Easy to extend
- Tool-agnostic

Each layer can be upgraded or replaced independently.

---

## Common Design Mistakes

- Sending logs directly to Elasticsearch
- No buffering layer
- Parsing everything in one place
- No clear ownership of stages

A SOC pipeline must be **designed**, not improvised.

---

## Key Takeaway

Start simple:
- rsyslog → Logstash → Elasticsearch

Add complexity only when needed:
- Kafka for scale
- Separate parsing services
- Multiple consumers

A good SOC pipeline grows with the organization.
