# Studio Docker Stack

Infrastructure for Studio operations, managed with Docker Compose + Git.

## Compose File Layout

- `compose.yaml`: shared base (project networks only)
- `studio-core.yaml`: runtime core (`mosquitto`, `node-red`)
- `studio-data.yaml`: data plane (`influxdb`, `telegraf`)
- `studio-monitoring.yaml`: observability (`prometheus`, `node-exporter`, `grafana`)
- `studio-infra.yaml`: edge/admin (`nginx-proxy-manager`, `portainer`, `authelia`)

Each service is defined in exactly one file to avoid duplicate definitions during merge.

## Run The Full Stack

```bash
docker compose \
  -f compose.yaml \
  -f studio-core.yaml \
  -f studio-data.yaml \
  -f studio-monitoring.yaml \
  -f studio-infra.yaml \
  up -d
```

## Run By Domain

```bash
# Core only
docker compose -f compose.yaml -f studio-core.yaml up -d

# Data only
docker compose -f compose.yaml -f studio-data.yaml up -d

# Monitoring only
docker compose -f compose.yaml -f studio-monitoring.yaml up -d

# Infra only
docker compose -f compose.yaml -f studio-infra.yaml up -d
```
