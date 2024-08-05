---
title: Monitoring your containers in docker
date: 2024-05-08 10:00
categories: [homelab, plex, media, docker, pmm, kometa]
tags: [homelab, plex, media, docker, pmm, kometa]
---

## Requirements
- Either one remote device like a raspberry pi or something that can run docker, or the existing host itself. 

## Getting Started
Though using the same device to monitor itself isn't always good practice as it doesn't show if remote connectivity is there etc. We can always use this to monitor the status of the containers and alert if they go offline etc. 

1) - As with the other documentation, open up dockge and hit compose. 
2) - Paste the following into the compose.yml window
```yaml
version: "3.3"
services:
  uptime-kuma:
    restart: always
    ports:
      - 3001:3001
    volumes:
      - uptime-kuma:/app/data
      - /var/run/docker.sock:/var/run/docker.sock
    container_name: uptime-kuma
    image: louislam/uptime-kuma:1
volumes:
  uptime-kuma: {}
networks: {}
```
3. - Hit save and then start the container up. 
4. - Enter a username and password. 
5. - Hit "Add new monitor"
![Uptime-kuma-new](/assets/img/uptime-kuma-new.png)
6. - Select Docker Container and fill in the details 
    - Give it a friendly name, and then enter the container name.  
    to get this, open a terminal window on your docker server and type `docker ps` then copy and paste the container name from the name column.
    - Add your docker host and then press save. 
7. You can now setup notifications if you want to. 
