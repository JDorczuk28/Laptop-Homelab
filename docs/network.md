# Networking

This covers the network-related setup

## Interface and IP

This server connects to my home network over WiFi
The main networking goals were:
- Connect the Ubuntu Server laptop to the home LAN
- Give the server a consistent IP address
- Allow SSH access from my main computer
- Allow VMs to communicate with the server
- Access web services such as Portainer and Nginx from another machine

## Interface

After installing, the interface was identified as 
```text
wlo1
```
which was found using:
```bash
ip a
```
The interface name is important because it's used in the netplan configuration

## Wifi Configuration

Ubuntu uses Netplan for network configuration
I found this file here"
```text
/etc/netplan/00-installer-config.yaml
```
The Wifi Configuration uses DHCP, which allows the router to assign the server an IP address
Example Netplan Config:
```yaml
network:
  version: 2
  wifis:
    wlo1:
      dhcp4: true
      optional: true
      access-points:
        "WIFI_NAME":
          password: "WIFI_PASSWORD"
```
Real WIfi name and password not included for obvious reasons
The updated netplan can be applied with:
```bash
sudo netplan generate
sudo netplan apply
```
Connection checked with:
```bash
ip a
ip route
```
A working connection should look like:
```text
inet 192.168.0.x/24
```

## DHCP Reservation 

I had to update my router's settings so that it keeps an IP address reserved for my server
This allows the server to have a static IP, so I don't need to recheck every time
Different ISPs will have different processes for this; mine was along the lines of checking a box and associating a MAC address with an IP.

## Local Network Access

The server is intended to be accessed only from the local home network.
No router port forwarding is currently configured.
This keeps services such as SSH, Portainer, and test containers private to the LAN.

## SSH

Once the server has a static IP, it can be accessed from other machines on the LAN through:
```bash
ssh USER@IP_ADDRESS
```
This allows for the server to be changed remotely, perfect as the computer it's hosted on doesn't have a working keyboard.

## Virtual Machine Networking

A Kali Linux VM was used to test access from another machine.
VM was set to a bridged adapter, which was set to my machine's real WiFi Adapter.
After switching to a bridged adapter, the VM should receive an IP address on the same LAN as the server.
You can test connectivity by:
```bash
ping SERVER_IP
```


