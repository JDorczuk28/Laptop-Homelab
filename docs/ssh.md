# SSH Access

This document covers how I access the Ubuntu laptop server remotely using SSH.

## Overview

OpenSSH Server was installed during the Ubuntu Server installation.
This allows me to manage the server remotely from a separate, working machine.

## Why SSH Is Important

The laptop being used as the server is partially broken, so local access is inconvenient.

With SSH, I can:

- Log into the server remotely
- Run Linux commands
- Update packages
- Manage Docker
- Restart or shut down the server
- Troubleshoot services

## Check SSH Status

To check whether SSH is running:
```bash
sudo systemctl status ssh
```

## Enable SSH on Boot

To make sure SSH starts automatically when the server boots:
```bash
sudo systemctl enable ssh
```

## Start SSH

If SSH is installed but not currently running:
```bash
sudo systemctl start ssh
```

## Connect From Another Machine

From my main computer or a VM, I can connect with:
```bash
ssh USERNAME@SERVER_IP
```

## Notes

SSH is only intended to be used on my local home network.
I am not forwarding port 22 from my router to the internet, or at least not yet.

The server will ask for a local login, but as long as it's running, this isn't needed; all services and functions can still be accessed remotely.
