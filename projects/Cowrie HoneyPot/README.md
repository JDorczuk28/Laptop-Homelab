# Cowrie HoneyPot
Cowrie is an SSH and Telnet honeypot used to capture and analyze unauthorized login attempts and command activity in a controlled lab environment.

## Goal
The goal of this project was to deploy a local honeypot using fake SSH and Telnet ports to capture would-be attackers and observe the logs as there ingested into Splunk.

## Ports 
To avoid interfering with the real SSH service, Cowrie was mapped to alternate host ports: 

Host Port	Cowrie Service	Container Port
2222	SSH honeypot	22
2323	Telnet honeypot	23

Testing happens through:
```bash
ssh -p 2222 root@SERVER_IP
```

## Directories
Before deploying the container, I created folders for Cowrie downloads, keys, logs, and terminal recordings:
```bash
sudo mkdir -p /home/jack/cowrie/downloads
sudo mkdir -p /home/jack/cowrie/keys
sudo mkdir -p /home/jack/cowrie/log/tty
```
Cowrie runs as UID and GID 2000, so the folders needed correct ownership:
```bash
sudo chown -R 2000:2000 /home/jack/cowrie
sudo chmod -R u+rwX /home/jack/cowrie
```

## Firewall
```bash
sudo ufw allow from 192.168.0.0/24 to any port 2222 proto tcp
sudo ufw allow from 192.168.0.0/24 to any port 2323 proto tcp
```
This allowed devices on my home LAN to reach the honeypot while avoiding broad public exposure.

## Log Collection
Cowrie writes structured event logs to:

/home/jack/cowrie/log/cowrie.json

The JSON log contains events such as:

- Connection attempts
- Source IP addresses
- Username attempts
- Password attempts
- Commands entered
- Session activity
- Download attempts

## Splunk

Cowrie logs were mounted into the Splunk container as read-only:

- /home/jack/cowrie/log:/cowrie-logs:ro

Inside Splunk, I added the following log file as a monitored input:

/cowrie-logs/cowrie.json

Example Splunk search for all Cowrie events:

index=main source="/cowrie-logs/cowrie.json"

Example search for command activity:

index=main source="/cowrie-logs/cowrie.json" eventid="cowrie.command.input"

## Testing
SSH test:
```bash
ssh -p 2222 root@SERVER_IP
```
Telnet test:
```bash
telnet SERVER_IP 2323
```
After connecting, I entered harmless commands such as:

- whoami
- pwd
- ls -la
- uname -a

I then used Splunk searching to make sure the logs are being ingested correctly.

## What I Learned
- How to deploy a Docker-based honeypot.
- How Docker host-to-container port mapping works.
- Why a honeypot should not conflict with the production SSH service.
- How to use UFW to limit honeypot access to a local network.
- How Cowrie records structured JSON security events.
- How to ingest honeypot logs into Splunk.
- How to search for captured command activity in Splunk.

