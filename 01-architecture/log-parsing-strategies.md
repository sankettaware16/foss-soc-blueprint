# Log Parsing Strategies in a FOSS SOC

Log parsing is one of the most critical and fragile components of a SOC.
Poor parsing leads to broken detections, lost fields, and unreliable alerts.

This document explains different parsing strategies and why
a microservice-based approach can outperform traditional GROK-based parsing.

---

## Traditional Parsing with GROK

GROK is commonly used inside Logstash to parse logs.

### Challenges with GROK

- Hardcoded patterns
- Difficult to modify existing rules
- Small log format changes break parsing
- Performance issues at scale
- Limited flexibility for unknown log formats

In growing environments, GROK becomes a maintenance bottleneck.

---

## Microservice-Based Parsing Approach

Instead of parsing logs inside Logstash, parsing logic is moved
into a dedicated parsing service.

### High-Level Flow

Log Sources  
→ rsyslog  
→ Kafka  
→ Parsing Microservice  
→ Elasticsearch  

---

## How the Microservice Model Works

1. Logs are collected and forwarded without parsing
2. A consumer service reads logs from Kafka
3. A dispatcher identifies log type
4. A matching parser processes the log
5. Structured JSON is produced
6. Parsed logs are forwarded to Elasticsearch

Unknown logs are handled by a fallback parser.

---

## Advantages Over GROK

### Dynamic Parsing
- Small format changes do not break parsing
- Regex-based logic is easier to maintain

### Plug-and-Play Parsers
- New log sources require only a new parser
- No changes to existing pipelines

### Better Scalability
- Parsing can scale independently
- Load can be distributed across services

### Improved Reliability
- Parsing failures do not block ingestion
- Logs are never dropped silently

---

## When This Approach Makes Sense

- Medium to large SOCs
- Multiple log sources
- Frequent format changes
- ML or enrichment pipelines
- High reliability requirements

---

## When GROK Is Still Enough

- Very small environments
- Few stable log sources
- Low log volume

---

## Key Takeaway

Parsing is not just a technical task — it is a design decision.

As SOC complexity grows, moving parsing logic out of Logstash
provides better flexibility, scalability, and long-term stability.
