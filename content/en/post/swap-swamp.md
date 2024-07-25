---
title: "Swap Swamp"
date: 2024-07-25T12:53:14-04:00
description: "Linux Swap Swamped by Baloo"
featured_image: '/images/posts/ai_generated/penguin_in_swamp.png'
tags: ["Linux", "Swap", "file indexing", "baloo"]
---

# Swap Swamped by Baloo 🐧

A short story about how my Linux swap file was swamped by the Baloo file indexer.

<!--more-->

There was no noticeable performance hit on the system, and by chance had noticed that the swap file was being used more than I would have liked. The system has 128GB of RAM and the swap file was being used even when there was plenty of RAM available. The system was running KDE Plasma and the Baloo file indexer was the culprit.

## The Problem
The swap file being full is not a problem in itself, but it did make me curious as to why it was being used.
```bash
free -h
               total        used        free      shared  buff/cache   available
Mem:           125Gi        12Gi        74Gi       399Mi        40Gi       113Gi
Swap:          511Mi       511Mi       100Ki
```

512MB of swap didn't seem like allot considering the amount of RAM available, so increased it to 10GB.

First turn off the swap file.
```bash
sudo swapoff /swap/swapfile
````
Then increase the size of the swap file using dd.
```bash
sudo dd if=/dev/zero of=/swap/swapfile bs=1M count=10240 oflag=append conv=notrunc 
````
Then create the swap file and turn it back on.
```bash
sudo mkswap /swap/swapfile
sudo swapon /swap/swapfile
````

After increasing the swap file size it was quickly populated with data and leveled out at around 900MB
```bash
free -h
               total        used        free      shared  buff/cache   available
Mem:           125Gi        12Gi        64Gi       397Mi        51Gi       113Gi
Swap:           10Gi       845Mi       9.7Gi
```

That was fine, but watching the swap file usage in [btop](https://github.com/aristocratos/btop) constantly growing and shrinking was annoying as the swap file lives on an SSD and I didn't want to wear it out.

## What is using Swap Space?
To find out what was using the swap space I used a simple bash command that doesn't require root privileges to list the processes using swap space and sort the result from the largest to the smallest.
```bash
for file in /proc/*/status; do awk '/VmSwap|Name/{printf $2 " " $3}END{ print ""}' $file; done | sort -k 2 -n -r | less
```

The output showed that baloo_file_extr and baloo_file indexer were using all the swap space.

## Baloo File Indexer
[Baloo](https://community.kde.org/Baloo) is the file indexer used by KDE Plasma, it indexes files and folders to make searching for files faster. On Manjaro (and most other distros) the Baloo file indexer is configured to index the user home directory.

There was no issue with Baloo, it was operating as expected. It was just a bit overwhelmed by the amount of small files in my development folders which lead to the swap file being used. To address this I configured Baloo to ignore the development folders and a couple other folders such as the steam directory. Afterward the swap file usage dropped dramatically.
```bash
free -h
               total        used        free      shared  buff/cache   available
Mem:           125Gi        13Gi        64Gi       389Mi        49Gi       112Gi
Swap:           10Gi       7.2Mi        10Gi
```

The indexer settings can be changed in the KDE System Settings under the "Search" section.
{{< figure src="/images/posts/screenshots/Indexer_Settings.png" title="KDE File Search Settings" >}}
