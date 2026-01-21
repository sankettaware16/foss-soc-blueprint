# High-Level FOSS SOC Architecture

A typical FOSS SOC consists of the following layers:

1. Log Sources (servers, applications, network devices)
2. Log Collection & Transport
3. Parsing & Normalization
4. Storage & Search
5. Detection & Alerting
6. Incident Response

## Example Data Flow

Application / System Logs  
 Log Shipper (rsyslog, beats, agents)  
 Log Processing (Logstash)  
 Storage (Elasticsearch)  
 Visualization (Kibana)  
 Alerting & IR (TheHive, Email, ChatOps)

Architecture should be adapted based on scale, compliance, and risk profile.
