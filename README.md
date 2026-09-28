# Home Server Infrastructure

Docker Compose stack for self-hosted services.

## Services

| Service | Image | Description |
|---------|-------|-------------|
| proxy | jc21/nginx-proxy-manager:latest | Reverse proxy with SSL (ports 80, 443, 81) |
| local-ecr | registry:2 | Private Docker registry with CORS and delete enabled |
| git | codeberg.org/forgejo/forgejo:16 | Self-hosted Git server |
| runner | data.forgejo.org/forgejo/runner:13 | CI/CD runner for Forgejo |
| runner-lite | data.forgejo.org/forgejo/runner:13 | CI/CD runner using config-lite.yml |

## Usage

```bash
docker compose up -d
```

## Network

All services share a single bridge network (`stack-network` / `shared-proxy-network`).

## Volumes

| Service | Host Path | Container Path |
|---------|-----------|----------------|
| proxy | /cloud/Docker/proxy/data | /data |
| proxy | /cloud/Docker/proxy/letsencrypt | /etc/letsencrypt |
| local-ecr | /cloud/Registry | /app/lib/registry |
| git | /cloud/Docker/git/config | /data |
| runner | /cloud/Docker/git/config/runner | /data |
| runner | /var/run/docker.sock | /var/run/docker.sock |
| runner | /usr/bin/docker | /usr/bin/docker (ro) |
| runner-lite | /cloud/Docker/git/config/runner | /data |
| runner-lite | /var/run/docker.sock | /var/run/docker.sock |
| runner-lite | /usr/bin/docker | /usr/bin/docker (ro) |

## Ports

| Port | Service | Purpose |
|------|---------|---------|
| 80 | proxy | HTTP |
| 443 | proxy | HTTPS |
| 81 | proxy | Admin UI |
