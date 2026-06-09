## UFW Firewall Rules

UFW was configured to allow access only from the local LAN and the Tailscale interface.

Allowed ports:

- `22/tcp` - SSH
- `8081/tcp` - Nextcloud
- `9443/tcp` - Portainer
- `3001/tcp` - Uptime Kuma

Allowed sources:

- `192.168.0.0/24` - home LAN
- `tailscale0` - private Tailscale network

Broad `Anywhere` rules were removed to reduce unnecessary exposure.


<img width="501" height="264" alt="image" src="https://github.com/user-attachments/assets/3a22f6b2-c41f-4b5e-9d00-15581434885f" />
