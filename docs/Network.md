# Networking

This covers the network-related setup

# Interface and IP

This server connects to my home network over WiFi
The main networking goals were:
- Connect the Ubuntu Server laptop to the home LAN
- Give the server a consistent IP address
- Allow SSH access from my main computer
- Allow VMs to communicate with the server
- Access web services such as Portainer and Nginx from another machine

# Interface

After installing, the interface was identified as 
```text
wlo1
```
which was found using:
```bash
ip a
```
