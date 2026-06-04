# Home Server Infrastructure

Docker Compose stack for self-hosted services.

## Services

| Service | Image | Description |
|---------|-------|-------------|
| proxy | jc21/nginx-proxy-manager | Reverse proxy with SSL (ports 80, 443, 81) |
| local-ecr | registry:2 | Private Docker registry |
| ecr-ui | joxit/docker-registry-ui | Web UI for the Docker registry |
| git | forgejo | Self-hosted Git server |
| runner | forgejo/runner | CI/CD runner for Forgejo |

## Usage

```bash
docker compose up -d
```

## Volumes

All persistent data is stored under `/cloud/Docker/` and `/cloud/Registry/`.
