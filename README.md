Network Automation and Monitoring System

A fully containerised, open‑source monitoring and logging stack built around VictoriaMetrics and LibreNMS. It collects host metrics, aggregates logs, and automatically discovers network devices for fault alerting—all visualised through Grafana and served behind a lightweight reverse proxy.

## Key Features

- **Unified Observability** – Time‑series metrics and logs stored separately (VictoriaMetrics & VictoriaLogs), queried side‑by‑side in Grafana.
- **Lightweight Collection** – vmagent scrapes Prometheus‑compatible endpoints; Vector tails host and Docker logs without heavy agents.
- **Network Fault Management** – LibreNMS automatically discovers devices (Juniper, Arista, APC) via SNMP, polls them, and triggers alerts on outages.
- **Distributed Polling** – Dedicated LibreNMS dispatcher container offloads polling work, keeping the UI responsive.
- **Environment‑Driven** – All settings (retention, credentials, timezone) live in a single .env file no hard‑coded values.
- **Reverse Proxy Ready** – Web UIs (Grafana, VictoriaMetrics, LibreNMS) attach to an external proxy network, so they can be exposed via Nginx or Traefik with path‑based routing and SSL.
- **Read‑Only Host Access** – Node Exporter and Vector bind‑mount /proc, /sys, and log directories with :ro, preserving host security.

## Tech Stack

| Component               | Purpose                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| **VictoriaMetrics**   | Time‑series database for metrics storage and querying (PromQL compatible). |
| **VictoriaLogs**      | Log storage and query engine (supports Elasticsearch API).             |
| **vmagent**           | Metrics scraper (Prometheus‑compatible) – collects from node‑exporter, SNMP exporter, and VictoriaMetrics itself. |
| **Vector**            | Scrapes logs devices and exposes metrics for vmagent. |
| **Node Exporter**     | Host hardware and OS metrics (CPU, memory, disk, network, RAPL power). |
| **Grafana**           | Dashboarding and visualization for metrics and logs.                   |
| **LibreNMS**          |	Network discovery, SNMP polling, and alerting engine for outage detection.
| **LibreNMS Dispatcher**|	Distributed polling worker that executes SNMP checks on your network devices.
| **MariaDB**           |	Database backend for LibreNMS (stores device inventory, event logs, etc.).
| **Redis**             |	Caching and session store for LibreNMS (improves UI responsiveness).

---
