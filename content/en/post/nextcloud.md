+++
date = 2022-06-08T11:14:48-04:00
description = "Learn how to install and use Nextcloud"
featured_image = '/images/posts/Nextcloud_Logo.png'
tags = ["open source", "docker", "linux", "storage", "office software"]
title = "Your Own Cloud with Nextcloud"
+++

# Nextcloud ☁️

Regain control of your data while still being able to securely share and collaborate with others.
<!--more-->

[Nextcloud](https://nextcloud.com) provides so many features but really boils down to being an extendable productivity 
tool to organize your digital life.  

Nextcloud itself is installed onto a server or in other words any PC left running 24/7, from big servers with 
multiple processors and disks to a little raspberry pi. It can be accessed through a web browser or with native client 
applications on just about every platform from desktop to mobile, these are called the sync clients and handle talking 
to the server and automatically pushing and pulling files to the server. This is useful for backing up pictures from a 
phone or important documents on the computer.  

## Why Nextcloud
Why would someone want to use Nextcloud? If we go off the description of their website we use Nextcloud to take control 
of our data, "the self-hosted productivity platform that keeps you in control". What does that actually mean though? 
Are we not already in control of our data? The data on our phones we have a few different types of data such as contacts, images/videos, the news we read, the schedule from our 
calendar to name a few. All of which can be done in Nextcloud  

#### Files Docs & Images/Videos 📄 & 📷
Chances are that your phone is backing up to either Google or Apple and regardless of how you feel about all your 
personal pictures being stored on someone else's computer you're bound to reach the limit of how many image or videos 
that can be saved before having to pay a monthly or yearly fee for more storage. Nextcloud [Files](https://nextcloud.com/files/) 
stores the files and provides the ability to share files such as images, image albums, videos or even word documents and 
at a fraction of the cost. A plus with Nextcloud is that every shared file or album supports extra security features 
such as having the link expire after a week or a month, or by setting a password for viewing the link.  

#### News 📰
RSS feeds still exist and are still a great way to follow the news but there aren't many client or services for managing
RSS new feeds anymore. Nextcloud provides a plugin called [News](https://apps.nextcloud.com/apps/news) that lets users 
subscribe to and organize RSS/Atom feeds. Most sites provide RSS feeds, though they may just be a bit hard to find. 
The server pulls down the news articles as they come in and are viewable in the web browser or a dedicated 
Nextcloud News Apps on [Android](https://play.google.com/store/apps/details?id=de.luhmer.owncloudnewsreader&hl=en_US&gl=US) 
and [iPhone](https://apps.apple.com/us/app/nextnews/id1573041539).  

#### Calendar & Contacts 📅 & 📇
The calendar and contacts are part of [Nextcloud Groupware](https://nextcloud.com/groupware/) and synced between devices 
using an internet standard called [CalDav](https://en.wikipedia.org/wiki/CalDAV) and is accessible from a number of 
different applications including the ones that come included on most PCs and mobile devices.  

#### Talk 👥
The [Talk](https://nextcloud.com/talk/) is an amazing builtin feature that enables secure messaging and high quality 
voice/video chat over a web browser or mobile device. The features include private, group, public and password protected 
calls! Just invite somebody, a whole group or send a public link to invite others to the call. You can also share your 
screen with everyone on the call.  

#### More Features
Nextcloud really has a lot of features that come as part of the installation (to many to list here) and even more 
features can be found be added from with from the Apps browser found in the web browser by clicking the top right icon 
or can view the apps directly from the Nextcloud site at [apps.nextcloud.com](https://apps.nextcloud.com/?is_featured=true).  

## Installing 💾
Thanks to the awesome work of the devs and the power of docker installing Nextcloud with the best performance and 
security tweaks is super simple. The hard part will be preventing data loss which is doable but requires some 
continued effort.  

#### Data Management Risks ⚠️
Installing and running Nextcloud comes with risks and responsibilities. For most use cases the data for multiple users is 
being stored on this system and while data loss is preventable, system failure is likely for most systems. A good motto 
to go by for important data is that, if it doesn't exist in at least 3 different places it's as good as gone. This 
should be true of the Nextcloud install, there should be a backup of all the data on separate disks and one backup 
should be at a different physical location. If running the server locally this can be achieved by backing up to an 
external disk for the second copy and then sending/syncing that backup to the cloud as it is already deduplicated and 
encrypted saving disk space and preserving privacy for offsite storage of the 3rd copy.

#### Docker 🐳
Installing Nextcloud has been made surprisingly easy, boiling down to running just a single command to get it up and 
running. This is thanks to the [All-In-One Nextcloud Install](https://github.com/nextcloud/all-in-one) 
found on github. With a single command it will install Nextcloud, Nextcloud Office, a high performance backend caching 
mechanism to improve performance for Nextcloud Files, another high performance backend for Nextcloud Talk, an office 
suite, optional antivirus scanner, and a backup solution based on [BorgBackup](https://www.borgbackup.org).  

The single command to run Nextcloud can be run any on any operating system running Docker but would recommend installing
it on a dedicated machine running a Linux based operating system such as [Ubuntu](https://ubuntu.com) and then running [Docker-CE](https://docs.docker.com/engine/install/ubuntu/) 
not Docker-Desktop as Docker-Desktop runs everything inside a virtual-machine. To get the backups saved to an external 
USB hard-drive you'll want to plug it in and add it to the fstab, so it is automatically mounted on startup 
before beginning the installation.

To add the USB hard-drive to the fstab follow these instructions.

Plug it in and get the drive path
{{< highlight bash-session "linenos=false" >}}
df -th
{{< / highlight >}}

After determining the drive path put that in the fstab or get an even more reliable identifier for the fstab, the UUID 
which is unique for each drive and the drive path starting with /dev path could change between reboots.
{{< highlight bash-session "linenos=false" >}}
sudo blkid /dev/<drive path> | awk -F'"' '{print $2}'
{{< / highlight >}}

Make sure the folder /media/backup exists and is empty then add the following line to the bottom of the fstab with your 
UUID
{{< highlight bash-session "linenos=false" >}}
UUID=<your UUID> /media/backup auto nosuid,nodev,nofail 0 0
{{< / highlight >}}

To mount the drive and verify it is working
{{< highlight bash-session "linenos=false" >}}
mount -a
touch /media/backup/testFile
{{< / highlight >}}

After the backup drive has been set up go get the most upto date installation instructions on the 
[Nextcloud All In One README](https://github.com/nextcloud/all-in-one#how-to-use-this).
