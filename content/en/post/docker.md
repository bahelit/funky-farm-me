---
date: 2022-05-27T11:14:48-04:00
description: "Using docker and containers."
featured_image: '/images/posts/Docker_logo.png'
tags: ["open source", "docker", "linux"]
title: "Using Docker"
---

# Docker 🐳️

Using Docker and containers makes experimenting with new software quick and easy.  
<!--more-->

With only a couple commands we can download, run and remove all traces of pretty much any piece of software. Docker runs 
the programs in containers, basically little isolated boxes that you can poke holes into to share disk space or open to 
the internet. The containers can have access to dedicated "disk space containers" called volumes as a way to save data 
separate from the container with the application. Docker also provides functionality for defining multiple containers as 
one working unit by orchestrating multiple containers with docker compose.

## Basics
Installing [Docker](https://www.docker.com). If on MacOS or on Windows the only option is to install [Docker Desktop](https://www.docker.com/products/docker-desktop/), 
Linux users can choose between Docker Desktop and the Docker-CE edition. Recommend using Docker-CE for Linux users as the 
Docker Desktop For Linux runs Docker in a VM, [why Docker4L runs in a VM](https://docs.docker.com/desktop/linux/install/#why-docker-desktop-for-linux-runs-a-vm).  

[Install Docker-CE on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)  

Learn more by following the official documentation for building and running your 1st container at [Docker Getting Started](https://docs.docker.com/get-started/)  

#### Tweaks for Personal Use
After installing Docker-CE there's at least one tweak that should be made if you plan on running services from it, and 
that's the logging mechanism. Docker captures all the logs from the running containers and stores them but has drivers 
that explain how to store them, we'll be changing the "logging driver".  

Recommend using the [Local File logging driver](https://docs.docker.com/config/containers/logging/local/), which by 
default preserves 100MB of log messages per container and uses automatic compression to reduce the size on disk. 
The 100MB default value is based on a 20M default size for each file and a default count of 5 for the number of such 
files. Without enabling this driver Docker could potentially run a disk out of space with log data.  

The other tweak is more specific for users of the ZFS filesystem, Docker has a special storage driver for users of ZFS.
[ZFS](https://docs.freebsd.org/en/books/handbook/zfs/) is a next generation filesystem that supports many advanced 
storage technologies such as volume management, snapshots, check-summing, compression and deduplication, replication and 
more.  

When the ZFS driver is in use the base layer of an image is a ZFS filesystem. Each child layer is a ZFS clone based on a ZFS 
snapshot of the layer below it. A container is a ZFS clone based on a ZFS Snapshot of the top layer of the image it’s 
created from. One benefit of this is very efficient use of the disk space.  

[Enable the ZFS Storage Driver](https://docs.docker.com/storage/storagedriver/zfs-driver/)  

#### Stay Tuned
Now that we got this brief introduction to Docker out of the way we'll walk through how we use Docker for installing and 
maintaining long-running services used at the Funky Farm.
