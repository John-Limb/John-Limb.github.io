---
title: SMB Share from Ubuntu to windows
date: 2024-05-08 10:00
categories: [homelab, plex, media, docker, pmm, kometa]
tags: [homelab, plex, media, docker, pmm, kometa]
---

## Getting Started

### Installing Samba
`sudo apt update`  
`sudo apt install samba`

### Configure Samba
In a terminal window open the smb conf file.  
`sudo nano /etc/samba/smb.conf`

At the bottom of the file paste in - I will use media in this example
```shell
[sambashare]
    comment = Media
    path = /mnt/media
    read only = no
    browsable = yes
```
Then press `CTRL+x` to save and exit.  

Restart the SMB service
`sudo service smbd restart`  

Samba does not use builtin OS password you will need to make your own for samba.  (probably best to use the same usr name and password as OS user).  

`sudo smbpasswd -a username` - change username to the name of OS user.  
