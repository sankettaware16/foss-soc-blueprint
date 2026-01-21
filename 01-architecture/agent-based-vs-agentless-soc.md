# Agent-Based vs Agentless SOC Architecture

One of the most important SOC design decisions is how data is collected
from endpoints and servers.

This document compares agent-based and agentless SOC architectures
in a vendor-neutral manner.

---

## Agent-Based Architecture

### How It Works
- Software agents are installed on endpoints
- Agents collect logs and telemetry
- Data is forwarded to the SOC backend

### Advantages
- Rich endpoint visibility
- Built-in FIM and vulnerability data
- Easier initial deployment

### Risks and Limitations
- Agents often run with high privileges
- Increased attack surface
- Performance overhead
- Operational complexity at scale

---

## Agentless Architecture

### How It Works
- Native system logging is used
- Logs are forwarded via syslog or similar mechanisms
- Centralized collection and processing

### Advantages
- Minimal endpoint footprint
- Reduced privilege risk
- Easier to audit and maintain
- Works well for servers and infrastructure

### Limitations
- Less endpoint telemetry
- Relies heavily on log quality
- Requires good pipeline design

---

## Hybrid SOC Model

Most mature SOCs use a hybrid approach:

- Agentless logging for servers
- Agents where deep visibility is required
- Centralized correlation and detection

This balances visibility, security, and operational cost.

---

## Choosing the Right Model

Consider:
- Organization size
- Risk profile
- Compliance requirements
- Available manpower

There is no universal answer — architecture must fit context.

---

## Key Takeaway

SOC architecture should reduce risk, not introduce it.

Choosing between agent-based and agentless approaches
is a strategic decision that impacts security and operations.
