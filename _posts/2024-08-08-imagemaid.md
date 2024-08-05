---
title: Imagemaid
date: 2024-05-08 10:00
categories: [homelab, plex, media, docker, pmm, kometa]
tags: [homelab, plex, media, docker, pmm, kometa]
---

## Requirements
* Docker and dockge running on your device
* Ability to mount the Plex folder structure in docker.

If your docker containers are running on the same server as plex then you will be able to map the folder using local path, otherwise you will need to do an NFS mount and update your /etc/fstab file.  
In this instance docker is running on the same host as plex. 

## Begin
1) Open up Dockge (http://SERVER-IP:5001)  
2) Click the Blue "Compose button"
3) Enter the following yaml into the compose.yaml window.  
``` yaml
version: "2.1"
services:
  plex-image-cleanup:
    image: meisnate12/plex-image-cleanup
    container_name: plex-image-cleanup
    environment:
      - TZ=Europe/London #Change to your Timezone
    volumes:
      - /opt/stacks/imagemaid/config:/config
      - /path/to/plex/install:/plex:rw
    restart: unless-stopped
```
Click save but do not start.   
4. Change to the imagemaid folder and edit the .env file. It wont exist yet so you will have to create it.  
`cd /opt/stacks/imagemaid/config`  
`sudo nano .env`  
paste the following into the nano window  
```
PLEX_PATH=/plex
MODE=remove
SCHEDULE="05:00|weekly(sunday)"
PLEX_URL=http://192.168.1.12:32400
PLEX_TOKEN=123456789
DISCORD=https://discord.com/api/webhooks/###################/####################################################################
TIMEOUT=600
SLEEP=60
IGNORE_RUNNING=False
LOCAL_DB=False
USE_EXISTING=False
PHOTO_TRANSCODER=False
EMPTY_TRASH=True
CLEAN_BUNDLES=True
OPTIMIZE_DB=True
TRACE=False
LOG_REQUESTS=False
```

Change the plex_token and Plex_url to your server IP and Token.  
Save and then start the container