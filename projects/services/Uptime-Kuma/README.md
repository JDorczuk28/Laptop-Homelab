# Uptime-Kuma

Service used to monitor the uptime of other services and the router.

## Goal

The goal is to be able to monitor my services from a single dashboard.
This allows me to quickly see the status of services.

## Access

Uptime Kuma is available on the local network at:

```text
http://SERVER_IP:3001
```

## Deployment

The stack was deployed using Portainer:

```text
Portainer -> local environment -> Stacks -> Add stack -> Web editor
```

The Docker Compose file is stored in this project folder as:

```text
docker-compose.yml
```

## Storage

Uptime Kuma stores its data in a Docker volume:

```text
uptime-kuma-data
```

This allows monitor configuration and history to persist after the container restarts.

## Monitors

The first monitors added were:

- Nextcloud LAN access
- Nextcloud Tailscale access
- Portainer
- Nginx test container
- Router ping

## Example Monitor Targets

```text
Nextcloud LAN:       https://SERVER_IP:8081
Nextcloud Tailscale: https://TAILSCALE_IP:8081
Portainer:           https://SERVER_IP:9443
Nginx Test:          http://SERVER_IP:8080
Router:              192.168.0.1
```

For services using local self-signed HTTPS certificates, I enabled the option to ignore TLS/SSL certificate errors.


## What I Learned

- How to deploy a monitoring service with Docker Compose
- How to monitor local web services
- How to monitor services using self-signed certificates
- How to use ping monitors for network devices
- How Docker volumes preserve monitoring data
- How service monitoring helps troubleshoot a homelab
