# Prometheus and Grafana Setup

<img width="1910" alt="Screenshot 2024-11-29 at 6 52 32 PM" src="https://github.com/user-attachments/assets/5775a913-a625-49ca-a91f-4b7065f38301">


This repository contains a `podman-compose` setup for running Prometheus and Grafana to monitor metrics from a custom target.

## Table of Contents
- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Setup](#setup)
- [Custom Metrics Target](#custom-metrics-target)
- [Accessing the Services](#accessing-the-services)
- [Troubleshooting](#troubleshooting)

---

## Overview

- **Prometheus** is used to scrape and store metrics from a custom endpoint.
- **Grafana** is used to visualize metrics scraped by Prometheus.

The target for Prometheus is configured to scrape metrics from `http://192.168.11.109:8080/metrics`.

---

## Prerequisites

- [Podman](https://podman.io/) installed on your system.
- [Podman Compose](https://github.com/containers/podman-compose) installed.
- An accessible metrics target exposing Prometheus-compatible metrics.

---

## Setup

1. Clone this repository:
   ```bash
   git clone https://github.com/your-repo/prometheus-grafana.git
   cd prometheus-grafana
   ```

2. Start the containers:
   ```bash
   podman-compose up -d
   ```

3. Verify the containers are running:
   ```bash
   podman ps
   ```

---

## Custom Metrics Target

Prometheus is configured to scrape metrics from `http://192.168.11.109:8080/metrics`.

### Example of Valid Metrics Output
```text
# HELP temperature_celsius Temperature in Celsius
# TYPE temperature_celsius gauge
temperature_celsius 22.76
# HELP temperature_fahrenheit Temperature in Fahrenheit
# TYPE temperature_fahrenheit gauge
temperature_fahrenheit 72.97
# HELP humidity_percentage Humidity in percentage
# TYPE humidity_percentage gauge
humidity_percentage 37.29
# HELP pressure_hpa Pressure in hPa
# TYPE pressure_hpa gauge
pressure_hpa 977.23
```

If your metrics target does not include a proper `Content-Type` header, refer to the [Optional: Adding a Reverse Proxy](#optional-adding-a-reverse-proxy) section.

---

## Accessing the Services

- **Prometheus**: [http://localhost:9090](http://localhost:9090)
- **Grafana**: [http://localhost:3000](http://localhost:3000)

### Grafana Credentials
- Username: `admin`
- Password: `admin`

### Adding Prometheus as a Data Source in Grafana
Prometheus is pre-configured as the default data source. If needed:
1. Navigate to **Configuration > Data Sources**.
2. Verify Prometheus is listed with the URL `http://127.0.0.1:9090`.

---

## Troubleshooting

### Prometheus Target Not UP
- Verify the target at `http://192.168.11.109:8080/metrics` returns valid Prometheus metrics:
  ```bash
  curl http://192.168.11.109:8080/metrics
  ```

- Check Prometheus logs:
  ```bash
  podman logs prometheus
  ```

### Grafana Not Accessible
- Verify the Grafana container is running:
  ```bash
  podman ps
  ```

- Check Grafana logs:
  ```bash
  podman logs grafana
  ```

---
