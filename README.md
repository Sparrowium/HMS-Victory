Network Automation and Monitoring System

## Overview
A lightweight, fully containerized monitoring and log‑aggregation platform built around VictoriaMetrics and LibreNMS. Metrics and logs are collected, stored, and visualised in a single Grafana interface, while LibreNMS handles traditional SNMP‑based device polling and alerting. All services are orchestrated via Docker Compose and configured through environment variables—ideal for homelabs, edge deployments, or any CLI‑friendly environment.

A separate reverse proxy (connected via the proxy external network) exposes the Grafana, VictoriaMetrics, and LibreNMS web UIs under a unified domain.
---

## Components

| Service               | Purpose                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| **VictoriaMetrics**   | Time‑series database for metrics storage and querying (PromQL compatible). |
| **VictoriaLogs**      | Log storage and query engine (supports Elasticsearch API).             |
| **vmagent**           | Metrics scraper (Prometheus‑compatible) – collects from node‑exporter, SNMP exporter, and VictoriaMetrics itself. |
| **Vector**            | Scrapes logs devices and exposes metrics for vmagent. |
| **Node Exporter**     | Host hardware and OS metrics (CPU, memory, disk, network, RAPL power). |
| **Grafana**           | Dashboarding and visualization for metrics and logs.                   |
| **LibreNMS**          |	Network discovery, SNMP polling, and alerting engine for outage detection.
| **LibreNMS Dispatcher**	Distributed polling worker that executes SNMP checks on your network devices.
| **MariaDB**           |	Database backend for LibreNMS (stores device inventory, event logs, etc.).
| **Redis**             |	Caching and session store for LibreNMS (improves UI responsiveness).

---
