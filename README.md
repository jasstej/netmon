# NetMon - Application-Level Network Usage Monitor

> A lightweight, single-file network traffic monitoring daemon with real-time web dashboard, process-level traffic attribution, historical analytics, and alerting for Linux systems.

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Linux](https://img.shields.io/badge/Platform-Linux-green)
![FastAPI](https://img.shields.io/badge/FastAPI-Web%20Dashboard-009688)
![License](https://img.shields.io/badge/License-MIT-yellow)

---

## Overview

NetMon is an advanced application-level network monitoring solution that tracks bandwidth usage per process, user, and container in real time.

Unlike traditional interface-based monitoring tools, NetMon maps network traffic directly to the applications generating it and provides historical analytics, alerting, and a modern web dashboard.

---

## Features

### Real-Time Monitoring

* Live upload/download bandwidth statistics
* Per-process traffic attribution
* Active socket tracing
* User-level traffic tracking
* Docker container awareness
* WebSocket-powered live updates

### Historical Analytics

* Minute-level traffic storage
* Hourly aggregation
* Daily aggregation
* Monthly aggregation
* Top bandwidth consumer reports

### Security & Alerting

* Bandwidth threshold alerts
* Unknown process detection
* Alert history logging
* Configurable monitoring rules

### Web Dashboard

* Modern responsive UI
* Real-time charts
* Active applications table
* Active socket tracing
* Historical analytics
* Configuration management

### Data Export

* CSV Export
* JSON Export
* Printable Reports

---

## Architecture

```text
                    ┌─────────────┐
                    │ Packet      │
                    │ Sniffer     │
                    └──────┬──────┘
                           │
                           ▼
                ┌────────────────────┐
                │ Socket Resolution  │
                └─────────┬──────────┘
                          │
                          ▼
                ┌────────────────────┐
                │ Process Mapping    │
                └─────────┬──────────┘
                          │
          ┌───────────────┼───────────────┐
          ▼                               ▼
 ┌────────────────┐            ┌────────────────┐
 │ SQLite Storage │            │ Alert Engine   │
 └────────┬───────┘            └────────┬───────┘
          │                             │
          ▼                             ▼
     ┌────────────────────────────────────┐
     │ FastAPI Web Dashboard + WebSockets │
     └────────────────────────────────────┘
```

---

## Requirements

### Supported Platforms

* Ubuntu
* Debian
* Fedora
* Arch Linux
* Most Linux distributions

### Python

* Python 3.8+

### Privileges

For full packet attribution:

```bash
sudo python3 netmon.py
```

Without root privileges, NetMon automatically falls back to a mock testing mode.

---

## Installation

### Clone Repository

```bash
git clone https://github.com/yourusername/netmon.git
cd netmon
```

### Run

```bash
python3 netmon.py
```

NetMon automatically installs required dependencies:

```text
fastapi
uvicorn
websockets
```

---

## Usage

### Start NetMon

```bash
sudo python3 netmon.py
```

### Open Dashboard

Navigate to:

```text
http://localhost:8000
```

---

## Dashboard Sections

### Dashboard

* Live bandwidth graph
* Upload/download statistics
* Top applications
* Active connections

### History

* Last 24 Hours
* Last 7 Days
* Last 30 Days
* All-Time Analytics

### Alerts

* Bandwidth anomalies
* Unknown process activity
* Threshold violations

### Settings

Example configuration:

```json
{
  "alert_threshold_mb_s": 10.0,
  "check_unknown_process": true,
  "alert_unknown_process_threshold_mb_s": 1.0
}
```

---

## REST API

### Status

```http
GET /api/status
```

### History

```http
GET /api/history?range=24h
```

### Top Consumers

```http
GET /api/top?range=7d
```

### Alerts

```http
GET /api/alerts
```

### Export

```http
GET /api/export?range=30d&format=csv
```

---

## Database Schema

NetMon uses SQLite and automatically manages data retention.

### Tables

| Table           | Description                  |
| --------------- | ---------------------------- |
| traffic_raw     | Minute-level traffic records |
| traffic_hourly  | Hourly aggregated traffic    |
| traffic_daily   | Daily aggregated traffic     |
| traffic_monthly | Monthly aggregated traffic   |
| alerts          | Alert history                |

---

## Docker Support

NetMon automatically detects Docker containers through Linux cgroups.

Example:

```text
Application: python3
Container: nginx-prod
Traffic: 45.2 MB/s
```

---

## Security Considerations

NetMon:

* Does not inspect packet contents
* Only tracks metadata and bandwidth usage
* Stores data locally
* Uses SQLite
* Sends no telemetry

---

## Performance

Typical resource usage:

| Resource         | Usage                |
| ---------------- | -------------------- |
| RAM              | 15–50 MB             |
| CPU              | 1–5%                 |
| Disk             | Depends on retention |
| Network Overhead | Negligible           |

---

## Project Structure

```text
netmon/
├── netmon.py
├── netmon.db
└── README.md
```

---

## Use Cases

* Home server monitoring
* VPS bandwidth accounting
* Docker traffic auditing
* Security investigations
* Malware analysis environments
* Bandwidth troubleshooting
* Development labs
* Self-hosted infrastructure monitoring

---

## Roadmap

Future planned features:

* Prometheus Exporter
* Grafana Integration
* GeoIP Resolution
* Kubernetes Awareness
* Email Alerts
* Telegram Notifications
* Multi-Host Monitoring
* Traffic Classification

---

## License

MIT License

---

## Author

**Jasstej Singh Marwaha**

Cyber Security Researcher
AWS Certified
AIR 19 – Pentathon 2025 CTF

GitHub: https://github.com/JasstejTrace

---

⭐ If you find NetMon useful, consider starring the repository.
