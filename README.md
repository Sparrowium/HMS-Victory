Network Monitoring System

A fully containerised, open‑source monitoring and logging stack built around VictoriaMetrics and LibreNMS. It collects host metrics, aggregates logs, and automatically discovers network devices for fault alerting—all visualised through Grafana and served behind a lightweight reverse proxy.

## Key Features

- **Unified Observability** – Time‑series metrics and logs stored separately (VictoriaMetrics & VictoriaLogs), queried side‑by‑side in Grafana.
- **Lightweight Collection** – vmagent scrapes Prometheus‑compatible endpoints; Vector tails host and Docker logs without heavy agents.
- **Network Monitoring** – SNMP Exporter polls devices (Juniper, Arista, APC) via SNMP and collect data / triggers alerts on outages.
- **Environment‑Driven** – All settings (retention, credentials, timezone) live in a single .env file no hard‑coded values.
- **Reverse Proxy Ready** – Web UIs (Grafana, VictoriaUI) attach to an external proxy network, so they can be exposed via Nginx with path‑based routing and SSL.
- **Read‑Only Host Access** – Node Exporter and Vector bind‑mount /proc, /sys, and log directories with :ro, preserving host security.

## Tech Stack

| Component               | Purpose                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| **VictoriaMetrics**   | Time‑series database for metrics storage and querying (PromQL compatible). |
| **VictoriaLogs**      | Log storage and query engine (supports Elasticsearch API).             |
| **vmagent**           | Metrics scraper (Prometheus‑compatible) – collects from node‑exporter, SNMP exporter, and VictoriaMetrics itself. |
| **Vector**            | Scrapes logs devices and exposes metrics for vmagent. |
| **Node Exporter**     | Create an endpoint to expose hardware and OS metrics (CPU, memory, disk, network, RAPL power). |
| **SNMP Exporter**     | Create an endpoint to export Networks hardware and metrics (link status, link speed, bandwidth, flaps). |
| **Grafana**           | Dashboarding and visualization for metrics and logs. |

---
