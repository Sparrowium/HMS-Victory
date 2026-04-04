Network Automation and Monitoring System

## Overview

This project provides a lightweight, containerized **network automation and monitoring stack** using Docker. It serves as a central reverse proxy for all web services and collects SNMP metrics from network devices (Juniper SRX, Arista DCS, APC UPS, etc.), while also offering DNS monitoring via CoreDNS.

All configuration is managed through environment variables, with no GUI dependencies – ideal for CLI‑friendly homelabs or production edge deployments.

---

## Components

| Service               | Purpose                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| **Nginx**             | Reverse proxy with sub‑path routing for Grafana, VictoriaMetrics/Logs, and other projects. |
| **VictoriaMetrics**   | Time‑series database for metrics storage and querying (PromQL compatible). |
| **VictoriaLogs**      | Log storage and query engine (supports Elasticsearch API).             |
| **vmagent**           | Metrics scraper (Prometheus‑compatible) – collects from node‑exporter, SNMP exporter, and VictoriaMetrics itself. |
| **Grafana**           | Dashboarding and visualization for metrics and logs.                   |
| **SNMP Exporter**     | Scrapes SNMP data from network devices (Juniper, Arista, APC) and exposes metrics for vmagent. |
| **CoreDNS**           | Internal DNS server with caching, forwarding, and Prometheus metrics.  |
| **Node Exporter**     | Host hardware and OS metrics (CPU, memory, disk, network, RAPL power). |

---
