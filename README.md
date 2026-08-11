# SOC Monitoring Stack

A self-hosted monitoring and log aggregation stack for SOC (Security Operations Center) use, built with Docker Compose.

## Stack Components

| Service        | Purpose                                      | Default Port |
|----------------|-----------------------------------------------|---------------|
| **Grafana**     | Dashboards and visualization                  | `3000`        |
| **Prometheus**  | Metrics collection and storage                | `9090`        |
| **Loki**        | Log aggregation                               | `3100`        |
| **Promtail**    | Log shipper (feeds logs into Loki)            | -             |
| **Node Exporter** | Host-level system metrics for Prometheus    | `9100`        |
| **soc-web**     | Web front end / dashboard for the SOC stack   | *(update)*    |

> ⚠️ Update the port numbers above and the `soc-web` entry to match what's actually defined in `docker-compose.yml`.

## Prerequisites

- Docker
- Docker Compose (v2, i.e. `docker compose`, not `docker-compose`)

## Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/praveen-066/soc-monitoring.git
   cd soc-monitoring
   ```

2. Configure environment variables (if applicable):
   ```bash
   cp .env.example .env
   # edit .env with your own values (e.g. Grafana admin password)
   ```

3. Start the stack:
   ```bash
   sudo docker compose up -d
   ```

4. Verify all containers are running:
   ```bash
   sudo docker compose ps
   ```

5. Access the services:
   - Grafana: `http://localhost:3000`
   - Prometheus: `http://localhost:9090`
   - Loki (via Grafana as a data source, not usually browsed directly)

## Configuration Files

- `docker-compose.yml` — defines all services in the stack
- `prometheus.yml` — Prometheus scrape targets and configuration
- `promtail-config.yml` — Promtail log source and Loki push configuration

## Stopping the Stack

```bash
sudo docker compose down
```

To also remove volumes (⚠️ this deletes stored metrics/logs data):
```bash
sudo docker compose down -v
```

## Notes

- Default Grafana credentials should be changed on first login (`admin` / `admin` unless configured otherwise).
- Data volumes are excluded from version control via `.gitignore` — back them up separately if needed.

## License

*(Add a license if you intend to share or open-source this project.)*
