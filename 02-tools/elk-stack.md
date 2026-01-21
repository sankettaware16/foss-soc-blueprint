# ELK Stack in a FOSS SOC

The ELK Stack (Elasticsearch, Logstash, Kibana) forms the backbone of many
open-source SOC implementations.

It provides log storage, search, visualization, and the foundation for
detections and alerts.

---

## What Problem Does ELK Solve?

Organizations generate logs from:
- Servers
- Applications
- Firewalls
- Mail systems
- Web servers

ELK helps to:
- Centralize logs
- Search events quickly
- Visualize activity
- Build detections and alerts

Without a SIEM-like system, security teams operate blind.

---

## Components Explained Simply

### Elasticsearch
- Distributed search and storage engine
- Stores parsed and structured logs
- Enables fast search across millions of events

Used for:
- Log retention
- Investigations
- Detection queries

---

### Logstash
- Log processing and transformation engine
- Parses raw logs into structured fields
- Applies enrichment (geo-IP, normalization)

Used for:
- Log parsing
- Field extraction
- Data normalization

---

### Kibana
- Visualization and dashboard layer
- Used by analysts and management
- Supports dashboards, alerts, and investigations

Used for:
- SOC dashboards
- Threat hunting
- Incident analysis

---

## Where ELK Fits in SOC Architecture

Log Sources  
→ Log Shippers (rsyslog / beats / agents)  
→ Logstash  
→ Elasticsearch  
→ Kibana  
→ Alerts / IR tools

ELK acts as the **central visibility and analysis layer**.

---

## Common ELK Mistakes

- Using ELK without proper parsing
- No index lifecycle management
- Storing too many fields blindly
- Treating ELK as a “set and forget” tool

ELK requires **design and tuning**, not just installation.

---

## When ELK Is Enough

- Small to mid-size organizations
- Universities and NGOs
- Centralized infrastructure
- Limited compliance requirements

---

## When ELK Needs Help

- Large environments → add Kafka
- Endpoint visibility → add Wazuh
- Network visibility → add Suricata / Zeek
- Case management → add TheHive

ELK is the core, not the whole SOC.

---

## Why ELK Is Popular in FOSS SOCs

- Free and open-source
- Massive community
- Flexible architecture
- Scales from single server to clusters

With proper architecture, ELK can rival commercial SIEMs for many use cases.
