# Tailscale Remote Access

This document covers how Tailscale was added to the homelab server for private remote access.

## Goal

The goal of adding Tailscale was to enable remote access for my homelab server so I can use services outside of my LAN without exposing anything directly to the internet.

## What is Tailscale

Tailscale is a mesh VPN that allows me to connect chosen devices on a private network, allowing them to communicate directly point-to-point without needing to open ports or configure a firewall.

## Install

Tailscale was installed on my ubuntu server with 
```bash
curl -fsSL https://tailscale.com/install.sh | sh
```

The server was then authenticated with:
```bash
sudo tailscale up
```

This produces a URL for me to visit and approve the server as a device.

## Tailscale Status

The status of tailscale can be checked by doing 
```bash
tailscale status
```

This shows the connected devices on the Tailnet and the relevant IPs
The server IP can be read from here or for more clarity, you can run 
```bash
tailscale ip -4
```

which will display the relevant IP to access services on the server.

## Scope
I plan to use Tailscale often in order to make services accessible from remote access, such as Nextcloud, and scale my homelab outside of LAN access only so I can access any service from anywhere.

## Security Notes

No port forwarding is used, the only way to access services is through my LAN or Tailscale-approved devices.



