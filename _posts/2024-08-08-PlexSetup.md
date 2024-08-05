---
title: plex setup
date: 2024-05-08 10:00
categories: [homelab, plex, media, docker, pmm, kometa]
tags: [homelab, plex, media, docker, pmm, kometa]
---

We are going to be setting up plex on a bare metal device, this can also be done with GPU passthrough to a Virtal machine if you want to.

## Requirements

- One device capable of Running plex (Preferably I5 6th Gen onwards for Quicksync etc) 16GB of Ram, Stand alone boot drive and a stand alone drive for media.
- Fixed IP address, either by reservation or out of your DHCP pool.
- A device capable of SSHing to the server (W10 and above or mac).
- Make sure all disks you want to use are installed and plugged in.

## Getting Started

#### Fire up an ubuntu install

1. Start up an ubuntu live CD, either Ubuntu Desktop or Ubuntu Server - Server is preferred as there is less Disk space and RAM used by OS
2. When at the installer screen you will want to Select "custom Storage layout" ![UbuntuDiskLaout](/assets/img/UbuntuDiskLayout.png)
3. On the disk you wish to use as OS, scroll to "Free space" and hit return and then "Add GPT partition", Scroll down and press "Create" - This will create your main OS disk ![UbuntuDiskLaout](/assets/img/UbuntuDiskLayout-OS.png)
4. On the disk you wish to use for media, scroll to "Free Space" and hit Return and then "Add GPT Partition", scroll down and on the mount point scroll to "other" and type `mnt/media` and then create
   ![UbuntuDiskLaout](/assets/img/UbuntuDiskLayout-Media.png)
5. Your disk layout should look something like this
   ![UbuntuDiskLaout](/assets/img/UbuntuDiskLayout-Complete.png)
6. Hit "Done" and then "continue" you will then be asked to give your server a name and enter usernames and passwords.
   Skip the ubuntu pro install, and then install OpenSSH Server so we can access later. - Hit done on the next two prompts and start the install

---

end
