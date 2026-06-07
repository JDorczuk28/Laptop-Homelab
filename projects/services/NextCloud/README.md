# NextCloud Local Cloud Storage

This project is a local-only cloud storage using a NextCloud Instance on my Ubuntu home server.

## Goal

The goal of this project is to create a private, local-only cloud storage as well as get me more familiarized with containers and managing them.

## Overview

I used NextCloud as a web-based file storage.
I used a MariaDB instance as the database for NextCloud.
I used Portainer in order to containerize and deploy the stack for this project.

## Services Running

Nextcloud - a web-based file storage application

nextcloud-db - MariaDB database used by Nextcloud

## Deployment

The stack was deployed using Portainer:
```text
Portainer -> local environment -> Stacks -> Add stack -> Web editor
```
The Docker Compose file is stored in this project folder as:
```text
docker-compose.yml
```
Resources needed to create this YAML can be found on Docker Hub.
## Database

The database is set up when configuring Nextcloud for the first time; the information used was the details included in the YAML file used to create the stack.

<img width="327" height="99" alt="image" src="https://github.com/user-attachments/assets/63dbb49e-9b53-4772-b7bc-494edb6f56cc" />

NextCloud stores uploaded files in a Docker volume on the server, and MariaDB stores database data in a separate Docker volume on the server

This means uploaded material will persist after restarts or outages.

## Testing

In the web interface, I create a new test folder as well as a picture of a panda (panda.jpeg)
<img width="744" height="550" alt="image" src="https://github.com/user-attachments/assets/198b38e4-3fa5-4eb6-a1bf-938e20319635" />

From here, I reboot the server and then SSH in as my user.
From here, we can view the different Docker volumes.
<img width="313" height="93" alt="image" src="https://github.com/user-attachments/assets/cd898933-11f8-405c-996e-c99ba5ab366f" />

By inspecting the data volume, we can find the mountpoint where everything is stored.
<img width="939" height="276" alt="image" src="https://github.com/user-attachments/assets/7e3bcc4b-ba04-4dfe-be92-b3664d5d073b" />

Then I can simply visit the mountpoint, traverse the files, and find where my files are stored. 
<img width="1565" height="37" alt="image" src="https://github.com/user-attachments/assets/54277304-b20f-4f4a-a409-978d30690496" />

## TailScale Addition

After confirming that Nextcloud worked locally, I downloaded Tailscale on my server for remote access outside of my LAN
Tailscale allows approved devices to access my Nextcloud without exposing everything to the public, keeping my files safe.

Access changes from
```text
https://SERVER_IP:8081
```

to

```text
https://TAILSCALE_IP:8081
```

## Trusted Domains

Nextcloud needs to trust each IP used to access it
My server IP was already trusted, but I had to add the tailscale IP generated for me to that list using:
```bash
docker exec -it nextcloud php /app/www/public/occ config:system:set trusted_domains 2 --value=TAILSCALE_IP
```

This allows me to be able to visit Nextcloud from the Tailscale IP on approved devices.


## Scope
This is currently set up for LAN and remote access using approved devices through Tailscale; 

## What I learned

- How to deploy a multi-container app using Docker Compose
- How Nextcloud uses a database and persistent file storage
- How Docker volumes store application data
- How containers communicate using service names
- How to access a self-hosted web app from other devices on the LAN
- How to troubleshoot database connection settings during setup
- Tailscale install and setup
- Adding trusted domains to Nextcloud config for remote access

## Status

- [x] Deployed Nextcloud stack
- [x] Created Nextcloud admin account
- [x] Connected Nextcloud to MariaDB
- [x] Uploaded test files
- [x] Verified local LAN access
- [x] Test persistence after full server reboot
- [x] Add Tailscale remote access




