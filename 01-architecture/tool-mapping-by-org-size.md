# SOC Architecture: Tools and Where They Fit in an Organization

There is no single “perfect” SOC architecture.
The right design depends on organization size, risk, and budget.

This document explains **how SOC architecture evolves** and
**which open-source tools fit at each stage**.

---

## Core SOC Building Blocks

Every SOC, regardless of size, needs:

1. Log collection
2. Central storage & search
3. Detection logic
4. Alerting & investigation
5. Incident response

The difference lies in **scale and depth**.

---

## Small Organizations (Startups, NGOs, Small Colleges)

### Typical Characteristics
- 5–50 servers
- Limited budget
- No dedicated SOC team
- Basic compliance needs

### Recommended Architecture

Log Sources  
→ rsyslog / Filebeat  
→ Logstash  
→ Elasticsearch  
→ Kibana  
→ Email alerts

### Tools That Fit
- ELK Stack → Central logging & visibility
- rsyslog / Filebeat → Log shipping
- Basic alerting in Kibana

### Why This Works
- Simple to operate
- Low resource usage
- Covers 70–80% of common threats

---

## Medium Organizations (Universities, SaaS, Growing Companies)

### Typical Characteristics
- 50–500 servers
- Dedicated IT/Security staff
- Compliance or audit pressure
- Internet-facing services

### Recommended Architecture

Log Sources  
→ Log Shippers  
→ Logstash  
→ Elasticsearch  
→ Kibana  
→ Wazuh / Alerting  
→ TheHive (optional)

### Tools That Fit
- ELK Stack → Central SIEM layer
- Wazuh → Host-based monitoring
- TheHive → Case management
- MISP → Threat intelligence (optional)

### Why This Works
- Adds endpoint visibility
- Enables structured incident handling
- Still cost-effective and open-source

---

## Large Organizations (Enterprises, Research Networks)

### Typical Characteristics
- 500+ servers
- Multiple environments
- High log volume
- Dedicated SOC team

### Recommended Architecture

Log Sources  
→ Kafka  
→ Logstash  
→ Elasticsearch Cluster  
→ Kibana  
→ Detection Engine  
→ SOAR / IR tools

Network Traffic  
→ Suricata / Zeek  
→ ELK

### Tools That Fit
- Kafka → Log buffering & scale
- ELK Cluster → High-volume SIEM
- Wazuh → Endpoint security
- Suricata / Zeek → Network detection
- TheHive + MISP → IR & threat intel

### Why This Works
- Handles scale and spikes
- Prevents data loss
- Supports advanced detections

---

## Where Each Tool Fits (Quick Mapping)

| Tool        | Purpose                         | Org Size |
|-------------|----------------------------------|----------|
| rsyslog     | Basic log forwarding             | Small+   |
| Filebeat    | Structured log shipping          | Small+   |
| Logstash    | Parsing & normalization          | All      |
| Elasticsearch | Storage & search               | All      |
| Kibana      | Visualization & analysis         | All      |
| Wazuh       | Host-based security              | Medium+  |
| Kafka       | High-scale log transport         | Large    |
| Suricata    | Network threat detection         | Medium+  |
| Zeek        | Network behavior analysis        | Large    |
| TheHive     | Incident response management    | Medium+  |
| MISP        | Threat intelligence              | Medium+  |

---

## Key Architectural Principle

Start **simple**, then **add layers**.

A good SOC:
- Grows with the organization
- Avoids unnecessary complexity
- Focuses on visibility first, then detection

This approach minimizes cost while maximizing security value.
