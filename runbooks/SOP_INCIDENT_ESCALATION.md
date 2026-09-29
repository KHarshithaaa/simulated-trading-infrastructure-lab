# Operational SOP Runbook: Low-Latency Exchange Triage & Escalation

## 1. Overview
Standard Operating Procedure (SOP) for L1 Site Reliability and DevOps Engineers monitoring the trading infrastructure core services.

## 2. Severity Matrix & Incident Escalation
* **SEV-1 (Critical)**: Matching Engine down, NIC buffer drop rate > 2%, unhandled socket exhaustion.
  - Action: Page Primary On-Call Quant/DevOps engineer within 2 minutes. Open emergency bridge.
* **SEV-2 (High)**: Market Data Feed delay > 15ms, synthetic load generator packet loss.
  - Action: Execute log triage runbook, capture `ss -tan` socket dumps, create Jira incident ticket.
* **SEV-3 (Moderate)**: Telemetry scraping failure, single worker pod restart.
  - Action: Investigate Prometheus exporter endpoint, review Docker daemon events.

## 3. Standard Escalation Log Dump Format (Jira Ticket)
```text
Issue Summary: [SEV-2] Latency spike detected on FIX Client Gateway
Service Affected: client-gateway / matching-engine
Socket State: TIME_WAIT count elevated (> 2,500 sockets)
NIC Drop Delta: 0 rx_drops, 0 tx_drops
Action Taken: Executed scripts/nic_socket_audit.sh, verified limits.conf ulimit allocation.
Escalated To: Core Platform Dev Team / On-Call Engineer


