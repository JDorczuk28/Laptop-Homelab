# Troubleshooting

This document lists issues I ran into while setting up my Ubuntu laptop homelab server and how I fixed or worked around them.

## Wi-Fi DHCP Hung During Install

During the Ubuntu Server installation, the Wi-Fi setup reached the DHCPv4 step but did not successfully receive an IP address.
Instead of waiting indefinitely, I continued the installation without network access and configured networking after Ubuntu Server was installed.

## DHCP Reservation

The server uses DHCP, but I configured a DHCP reservation on my router.
This helps keep the server reachable at the same local IP address each time it connects to the network.

## Kali VM Could Not Reach the Server

When testing SSH from a Kali VM, the VM originally had an IP address on a different subnet:
```text
Kali VM: 192.168.20.x
Server:  192.168.0.x
```
This was due to a prior setup where I had it set to an internal network and statically set the IP address.
The fix was simply switching to a bridged adapter and getting an IP address assigned for my VM.

## Server Shutdown

The server is not intended to run 24/7.
When I am finished using it, I can shut it down remotely with:
```bash
sudo shutdown now
```
When powered back on, Ubuntu Server boots, SSH starts, Docker starts, and containers with restart policies come back automatically.
