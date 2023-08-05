+++
date = 2021-04-24T11:14:48-04:00
description = "Run self-hosted services"
featured_image = '/images/posts/hddsBlue.jpg'
tags = ["server", "docker", "linux", "ubuntu"]
title = "Home Server"
+++

# Home Server 🖥️

Running a home server can be a fun learning experience that can be done on just about any hardware. There doesn't have 
to be anything special about the hardware as it's the software running on the hardware the serves the data.  
<!--more-->

A [home server](https://en.wikipedia.org/wiki/Home_server) can come in many shapes in sizes, from the size of a credit
card to the size of a closet while still being fast enough to run multiple services for multiple users.  

## Data

When running server software the data is usually the most important part and running it locally places that
responsibility of losing that data on the user. This may be a bit scary at first but there is a couple of things that can 
be done to gain some confidence that total data loss is avoidable.  
* Redundancy
* Backups

#### Redundancy

If the hardware supports multiple disks there are multiple ways to get them to act as one disk, like mirror images of 
each other referred to as [RAID 1](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_1). This functionality can be 
provided by special cards with chips on them or by software at the user level like Windows [Storage Spaces](https://support.microsoft.com/en-us/windows/storage-spaces-in-windows-b6c8b540-b8d8-fb8a-e7ab-4a75ba11f9f2) 
or on Linux with [LVM](https://en.wikipedia.org/wiki/Logical_Volume_Manager_(Linux)) and at the system level with 
filesystems like [ZFS](https://en.wikipedia.org/wiki/ZFS) or [BTRFS](https://en.wikipedia.org/wiki/Btrfs). Having the 
data spread across multiple disks helps prevent data loss when a drive fails as it is unlikely that two drives would 
fail at the same time. When one drive fails hopefully the other keeps working until the failed drive is replaced.  

#### Backup

Redundancy can help with keeping the machine running when a disk fails, but in the worst case scenario such as fire or 
flood both drives would be bad and all the data would be lost. If this is a concern an "offsite" backup could be setup.
While this kinda defeats the purpose of "self-hosting" it is just kinda hard getting around having to store at least a 
copy (encrypted copy) of important data on "someone else's computer" to help prevent data loss.

## Hardware

The options in hardware can be quite daunting, but it really only takes a few building blocks to get a system up and 
running
* Processor - how fast can it do things
* Memory - how many things can it do at once
* Storage - how many photos/recordings/documents can it hold
* Power Supply - how much energy will it consume

### Old PC

A good place to start for a home server would be to repurpose an old computer. While an old phone or tablet could also be 
repurposed the device itself isn't tuned for that use case and could overheat depending on the usage and local climate. 
The other thing to consider with phones or tablets is the available software to run, some devices are restricted to 
the apps available from the devices "app store" which may be lacking in useful server "apps".

### Raspberry Pi

The [Raspberry Pi](https://en.wikipedia.org/wiki/Raspberry_Pi) is one of the cheapest, easiest and energy efficient 
routes to get started running services. The [Raspberry PI Zero 2](https://www.raspberrypi.com/products/raspberry-pi-zero-2-w/) 
at $15 has a 1GHz quad-core processor with half a gigabyte of memory and max power draw of 3 watts, the [Raspberry Pi 4](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/) 
at $35 has a 1.5GHz quad-core processor 2 gigabytes of memory and max power draw of 7.6 watts. These devices are known as 
single-board computers and have everything needed to start computing except the mouse/keyboard and screen. Both of these 
devices are a capable little "home servers", the pi 4 can even support 2 4k monitors and provide desktop functionality.

At the Funky Farm the raspberry pis are being used for automation services. For example, in the greenhouse they control 
the various lights and pumps based on a schedule and provide nutrients based on readings from probes and sensors with 
help from a piece of software called [Home Assistant](https://www.home-assistant.io/).

### NAS

A [NAS](https://en.wikipedia.org/wiki/Network-attached_storage) (network attached storage) is a file server that plugs 
into the router, they can be small devices that use very little power, from 60 to 90 watts depending on how many drives 
are supported. These are special purpose built devices that come with low power usage processors and slots for multiple 
hard drives that allows for easy configuration of getting the hard drives setup as mirror images of each other or other 
RAID configurations. They come ready to back up files from other PCs or mobile devices and usually also provide an app 
store to easily install server related software. While major NAS brands like [Synology](https://www.synology.com/en-us/products/series/home) 
or [Q-NAP](https://www.qnap.com/en-us/product/series/home) make devices that in a variety of sizes and price ranges, 
even the cheapest of these devices without drives is still expensive. The NAS devices themselves can be pretty simple, 
being made up of just a shell to hold drives with a low powered SOC and a two-bay NAS can be found for 
around $100, without the drives. The more expensive ones are going to be faster but also have better software for 
managing the drives and data.

### Custom Build

We have a custom build at Funky Farm that is built primarily for data storage, our PCs and phone's automatically back-up 
everything from contacts to videos to the Funky Farm server instead of the cloud (Apple, Google). This use case 
could be covered by a NAS, but building a PC/Server allows for even more control over the whole experience, which could 
be cheaper than buying a NAS or paying for cloud storage.

The parts were carefully selected based on good experiences with the brands. 

* [AMD 3700x](https://www.amd.com/en/products/cpu/amd-ryzen-7-3700x) - processor 
* [Asus Pro WS X570-ACE](https://www.asus.com/us/Motherboards-Components/Motherboards/Workstation/Pro-WS-X570-ACE/) - AMD workstation motherboard 
* [Samsung DDR4](https://www.samsung.com/semiconductor/dram/module/M378A4G43AB1-CWE/) - ECC memory
* [Intel Optane NVME SSD](https://www.intel.com/content/www/us/en/products/sku/97544/intel-optane-memory-series-16gb-m-2-80mm-pcie-3-0-20nm-3d-xpoint/specifications.html) - storage cache 
* [SanDisk SSD](https://www.westerndigital.com/products/internal-drives/sandisk-ssd-plus-sata-iii-ssd#SDSSDA-120G-G25) - fast storage
* [WesternDigital Red NAS HDD](https://www.westerndigital.com/products/internal-drives/wd-red-plus-sata-3-5-hdd#WD40EFZX) - file storage
* [LSI SAS 9207-8i](https://www.broadcom.com/products/storage/host-bus-adapters) - storage controller (allows for more HDDs/SDDs to be added)
* [EVGA SuperNOVA 650 GA](https://www.evga.com/products/product.aspx?pn=220-GA-0650-X1) - power supply (10-year warranty)
* [ENTHOO PRO 2](https://www.phanteks.com/Enthoo-Pro2-Closed.html) - desktop style case to hold the parts

The system runs [Ubuntu](https://ubuntu.com/) and is installed on 2 SSDs each a mirror of the other in case one fails. 
The hard drives are also installed in pairs of 2 and the system is told to see them as one drive, with each pair of 2 
drives being mirror images of each other. Since hard drives are pretty slow the Intel Optane drives (really fast) 
acts sort of as a cache for the data on the drives making the system feel faster than the hard drives can alone while 
still having lots of storage for a lower cost. This level of configuration on the system drives is powered by the ZFS 
filesystem.  

The Funky Farm server runs all the services using containers with [Docker](https://www.docker.com/). This allows for 
running programs in a way that doesn't depend on what is installed on the host system or what the host operating system 
even is. Docker makes for a great tool for home servers, allowing for easy experimentation with complicated 
software with an easy way to clean-up afterwards.  

## Software

The software for a typical home server would handle the work of saving a file and serving a file. For example 
most NAS devices are configured to receive important files from other devices in the house for backup in case the hard 
drive on the device goes out. The simple backup software allows for the backup to happen automatically every time a new 
file is added or changed. If the NAS software supports snapshots the backup would protect against one of the worst type 
of attacks to be effected by, ransomware. Ransomware encrypts all the data on the machine and holds the keys to unlock 
the data ransom until payment has been made. Enabling snapshots essentially could save the data from being lost as 
the last copy before it was encrypted should still exist in the snapshot history.  

Saving and serving files plus the automation based on timers and sensor readings mentioned above are just scratching the 
surface. There are countless services/tasks that have already been built and just need to be installed and configured, 
just see this [awesome list of self-hosted projects](https://github.com/awesome-selfhosted/awesome-selfhosted) for ideas 
and look forward to articles about specific pieces of software or use-cases for the home server.
