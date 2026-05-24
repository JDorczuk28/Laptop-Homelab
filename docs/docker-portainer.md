# Docker and Portainer

This document covers the Docker and Portainer setup for my Ubuntu laptop homelab server.

## Overview

Docker is used to run services in containers.
Portainer is used as a web interface for managing Docker containers, images, volumes, networks, and stacks.
This makes it easier to manage the server without needing to run every Docker command manually.

## Docker Installation

Before installing Docker, I updated the package list:
```bash
sudo apt update
```

Docker was installed with:
```bash
sudo apt install -y docker.io
```

## Enable Docker on Boot

Docker was enabled so it starts automatically when the server boots:
```bash
sudo systemctl enable docker
```

Docker was started with:
```bash
sudo systemctl start docker
```

To check Docker status:
```bash
sudo systemctl status docker
```

## Test Docker

Docker was tested with:
```bash
sudo docker run hello-world
```

This confirms that Docker can pull and run containers.

## Docker Compose

This server uses Docker Compose v2.

The version can be checked with:
```bash
docker compose version
```

Because this is Compose v2, commands use:
```bash
docker compose up -d
```

not the older style:
```bash
docker-compose up -d
```

## Portainer Setup

A Docker volume was created to store Portainer data:
```bash
docker volume create portainer_data
```

Portainer was started with:
```bash
docker run -d \
  -p 9443:9443 \
  --name portainer \
  --restart=always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v portainer_data:/data \
  portainer/portainer-ce:latest
```

## Portainer Access

Portainer can be accessed from another machine on the same network at:
```text
https://SERVER_IP:9443
```

The browser may show a warning because Portainer uses a self-signed HTTPS certificate by default.
After opening Portainer for the first time, I created the initial admin account through the web interface.

## Local Docker Environment

Portainer was connected to the local Docker environment using the Docker socket:
```text
/var/run/docker.sock
```
This allows Portainer to manage Docker directly on the laptop server.

## First Test Stack

The first test stack deployed was an Nginx container.
The stack was added through:
```text
Portainer -> local environment -> Stacks -> Add stack -> Web editor
```

The stack file used:
```yaml
services:
  nginx:
    image: nginx:latest
    container_name: nginx-test
    ports:
      - "8080:80"
    restart: unless-stopped
```

After deployment, the Nginx test page was available at:
```text
http://SERVER_IP:8080
```

## Restart Policies

Containers use restart policies so they can come back after the server reboots.
Example:
```yaml
restart: unless-stopped
```
This means the container will restart automatically unless it was manually stopped.

## Notes

Portainer and the test containers are only intended to be accessed from my local home network.
No router port forwarding is currently configured.
The server is not intended to run 24/7. When the laptop server is shut down, Docker, Portainer, and all containers stop. When the server is powered back on, Docker starts again and containers with restart policies come back automatically.
