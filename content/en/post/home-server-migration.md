+++
date = 2023-07-25T11:14:48-04:00
description = "Migrating from a server OS acting as a NAS to a NAS OS for the server"
featured_image = '/images/posts/hddsBlue.jpg'
tags = ["server", "docker", "linux", "ubuntu", "TrueNAS SCALE", "ZFS", "NAS", "home server", "migration"]
title = "Home Server Migration"
+++

# Home Server Migration 💾

Are you tired of managing your containerized applications on Ubuntu with Docker? Are you looking for a more scalable and 
efficient solution? Look no further than TrueNAS SCALE, a powerful storage and computing platform that utilizes 
Kubernetes to manage containers. In this blog post, I will guide you through the process of migrating from Ubuntu with 
Docker to TrueNAS SCALE with Kubernetes.  
<!--more-->

Many years ago I tried to run TrueNAS on my desktop/server, but had issues with the setup. It is a great for my storage 
needs but has compatibility issues with my hardware making it a poor choice. On top of the hardware compatibility 
issues, I also had a desire to run Docker containers on the server, but with TrueNAS being based on FreeBSD that 
requires creating a virtual-machine and installing a Linux operating system to run the containers. While this was 
possible, it was not an ideal solution.  

#### Previous Setup
Since Docker has become an essential tool for my workflow personally and professionally, I decided to look for 
alternative solutions that would allow me to leverage both Docker and ZFS. After researching my options, I settled on 
Ubuntu Server, which supports the ZFS filesystem.  

One of the main advantages of moving to Ubuntu has been the ability to use Docker and ZFS. With the [Docker ZFS Driver](https://docs.docker.com/storage/storagedriver/zfs-driver/) 
the integration between Docker and ZFS allows for efficient use of disk space by utilizing clones and snapshots from the 
filesystem to stitch together the container layers. Plus, the abundance of documentation and community support 
surrounding Docker and Ubuntu has made troubleshooting and optimizing the setup much simpler.  

See the previous [Home Server]({{< ref "home-server.md" >}}) post for more information on the previous setup.  

## TrueNAS SCALE
Looking to make running my home server and storage system more simple I've been wanting to go back to TrueNAS and with 
the release of TrueNAS SCALE which is Linux based, decided it was time to make the jump.  

TrueNAS SCALE is a software-defined storage (SDS) platform developed by [iXsystems](https://www.ixsystems.com/). It is 
designed to provide a scalable, high-performance storage solution for modern data centers (and basements or closets 🤓), 
and is built on top of the OpenZFS file system. The list of features is a mile long and includes support for Docker, 
Kubernetes, and VMs, but I'll just focus on the ones that are most important to me which make supporting the Funky Farm 
easier.
* Integrated Linux Containers & VMs
* Deploy as a Single Node or Cluster
* Wide range of hardware support
* Ease of administration
* Data protection
* Data management

## Backup Validation 🖴
The data is the most important part of the server, so it is important to make sure it is backed up before making any
changes. I keep my data backed up with the 3-2-1 rule, data on the server is backed up to a separate drive on the server, 
but it is also backed up to a separate server in a different physical location. This is a good rule to follow to if you 
want to make sure your data is safe. At the Funky Farm we have an external drive plugged into the server that is used 
as a backup drive and once a week and before every software update the data is backed up to the external drive using 
[borgbackup](https://www.borgbackup.org/) which handles the deduplication and encryption of the data. Another backup is 
performed monthly that sends the encrypted backup to a server in a different physical location.  

A backup could be considered like Schrödinger's cat, it exists and doesn't at the same time, and we really don't know 
until we observe it that the backup exists. Before proceeding with the migration, we want to make sure to validate the 
backups. Validated my backups by removing the external drive from the server and plugging it into my PC. With Borg 
backup you are able to mount the encrypted backup as a filesystem and browse the files using the [borg mount](https://borgbackup.readthedocs.io/en/stable/usage/mount.html)
command. This allows for easy validation of the backup by checking that the files are there and can be read.  

## Installing TrueNAS SCALE

Installing TrueNAS SCALE is pretty straight forward, the [documentation](https://www.truenas.com/docs/scale/gettingstarted/install/installingscale/)
is very detailed and easy to follow but likely won't be needed for the installation part. The only thing to 
note is that I experienced issues getting the USB stick to boot, it was not appearing in the BIOS as a boot drive but 
after trying a different USB ports on the machine it was finally detected as a boot drive.  

After getting TrueNAS SCALE installed, the next step is to configure the storage. The storage is configured using the 
web interface which is very easy to use and has a lot of helpful documentation, start with the [Getting Started](https://www.truenas.com/docs/scale/gettingstarted/configure/)
page. Would recommend going with adding disks in pairs of two and configuring them as a mirror when adding them to a pool, 
this will allow for easy expansion and better performance. See the [storage documentation](https://www.truenas.com/docs/scale/scaletutorials/storage/) 
for more details.  

With a pool created the next step is to create the [datasets](https://www.truenas.com/docs/scale/scaletutorials/storage/datasets/). 
Datasets could be considered similar to folders but have more features such as limiting the amount of space they can 
consume, and setting compression per dataset. I have been creating a new dataset for each application that I run on the 
server, this allows for easy configuration of the disk space and permissions and makes it easier to identify the 
important data for backups, as the backup solution will to back up a whole dataset at a time.  

## Installing Docker 🐳
[Docker](https://www.truenas.com/docs/scale/scaletutorials/apps/docker/) is already installed, and you can start new 
Docker containers from the web interface, but I currently prefer to use the Apps provided by the catalog. While 
technically the Apps are running in Docker containers, they are managed by TrueNAS and run within a Kubernetes cluster. 
If an application is not available in the catalog, there is another catalog that can be added that has more application 
to choose from. [TrueCharts](https://truecharts.org/) is a community-driven catalog of Helm charts that can be added to 
TrueNAS SCALE. While I went with TrueNAS SCALE to use Docker without having to run a VM the Level1Techs video below 
shows how to do it.  

## Nextcloud 📁
On TrueNAS SCALE, there are multiple ways to run Nextcloud based on your needs. The Nextcloud team recommends running 
Nextcloud-AIO (suite of docker containers) inside a VM, this provides an easy deployment and maintenance with most 
features included in this one Nextcloud instance. The other option is to use the Nextcloud Helm chart from TrueCharts, 
this is the option I went with, it is more lightweight and less resource-intensive than the Nextcloud-AIO VM. The 
downside is that it does not include features like Calendar, Contacts, Mail, and Talk which are part of the [Groupware](https://nextcloud.com/groupware/) 
package. It does include the most important one user management and file storage. If you need the Groupware features 
you can follow this guide by Level1Techs to get it running in a VM and be able to connect to it remotely using Tailscale.  

[LEVEL1TECHS TRUENAS: FULL SETUP GUIDE FOR SETTING UP PORTAINER, CONTAINERS AND TAILSCALE](https://level1techs.com/video/truenas-full-setup-guide-setting-portainer-containers-and-tailscale-ultimatehomeserver)  

The reasons I currently prefer to use the [Apps](https://www.truenas.com/docs/scale/scaletutorials/apps/) is that they
are managed within TrueNAS using the web interface and with a couple of clicks can upgrade or even rollback a version.
The Apps also have a lot of custom configuration options exposed through the interface that make it easy to configure
the application being deployed.  

We use this Nextcloud this instance just to save our files and photos from our mobile devices using the auto-upload 
feature of the [Nextcloud Mobile App](https://nextcloud.com/clients/).  
{{< figure src="/images/posts/trueNAS_Deploy_Nextcloud.png" title="Deploying" >}}

## Nextcloud Cron Job ⌛
For the Nextcloud to function properly a cron job needs to be added, this is a scheduled task that executes a
command at a given frequency. To get this cron job to fire in TrueNAS SCALE we'll add a [Cron Job](https://www.truenas.com/docs/scale/scaleuireference/systemsettings/advancedsettingsscreen/#cron-jobs-widget) 
by going to "System Setting > Advanced", and clicking "Add" and putting the following command in the command field.
```bash
docker ps  | grep "k8s_nextcloud_nextcloud" | awk '{ print $1; }' | xargs -I % docker exec --user www-data "%" php -f /var/www/html/cron.php
```
My schedule is configured as every day every 5 minutes, there may be a better way to represent this but this is what I 
have.
``` bash
"5,15,25,35,45,55 * * * *"
```

## Migrating the Data 📁
With the storage configured and Nextcloud installed, the next step is to migrate the data from the old server. This could be 
done a few different ways like plugging the external drive into the new server and copying the data over into a dataset. 
With the main application being used on the server being Nextcloud, I decided to have the backup mounted on my PC with 
the borg mount command and then use the [Dolphin File Manager](https://apps.kde.org/dolphin/) (the default on Linux when using KDE)
to copy the data over the network to the new server using [Nextcloud's webdav](https://docs.nextcloud.com/server/latest/user_manual/en/files/access_webdav.html) 
interface. Migrating the data this way allowed me to start fresh with a new user and add my old data to the new user in 
an easy way.

## Conclusion
With the data migrated and the applications installed, the migration is complete. The new setup is much easier to 
manage and has a lot of room for expansion. The only thing missing is a backup solution, but that will be covered in a
future post.