# Home Server Infrastructure

Docker Compose stack for self-hosted services.

## Services

| Service | Image | Description |
|---------|-------|-------------|
| proxy | jc21/nginx-proxy-manager:latest | Reverse proxy with SSL (ports 80, 443, 81) |
| local-ecr | registry:2 | Private Docker registry with CORS and delete enabled |
| ecr-ui | joxit/docker-registry-ui:latest | Web UI for the Docker registry |
| git | codeberg.org/forgejo/forgejo:15 | Self-hosted Git server |
| runner | data.forgejo.org/forgejo/runner:12 | CI/CD runner for Forgejo |

## Usage

```bash
docker compose up -d
```

## Network

All services share a single bridge network (`stack-network`).

## Volumes

| Service | Host Path | Container Path |
|---------|-----------|----------------|
| proxy | /cloud/Docker/proxy/data | /data |
| proxy | /cloud/Docker/proxy/letsencrypt | /etc/letsencrypt |
| local-ecr | /cloud/Registry | /app/lib/registry |
| git | /cloud/Docker/git/config | /data |
| runner | /cloud/Docker/git/config/runner | /data |
| runner | /var/run/docker.sock | /var/run/docker.sock |

## Ports

| Port | Service | Purpose |
|------|---------|---------|
| 80 | proxy | HTTP |
| 443 | proxy | HTTPS |
| 81 | proxy | Admin UI |
