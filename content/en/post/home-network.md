---
date: 2021-04-23T11:13:32-04:00
description: "Home network configuration & recommendations"
featured_image: '/images/posts/home_networking.jpg'
tags: ["Home Network", "Wi-Fi", "DIY", "Tips", "DNS"]
title: "Home Network"
---

# Home Networking 🌐

Networking can be a complicated subject where mistakes can lead to security vulnerabilities at worst and bad performance, 
at best, this is true for businesses and homes of all sizes.  
 <!--more-->

Most home networks will consist of one connection to the WAN (internet) that all the devices in the local network, aka the [LAN](https://en.wikipedia.org/wiki/Local_area_network) 
use to access the internet. The [WAN](https://en.wikipedia.org/wiki/Wide_area_network) connection comes from the [modem](https://en.wikipedia.org/wiki/Modem) 
which handles talking to the internet service provider (Comcast, Spectrum, StarLink). Most internet service providers 
will "provide" (rent) a modem and that modem my include a [router](https://en.wikipedia.org/wiki/Residential_gateway). 
The LAN connections are managed by the router, all the devices talk to the router, wired or Wi-Fi and the requests for 
the internet get "routed" through the modem to access the internet.

When devices connect to the router one of the things the router tells the devices about it, is who to talk to for 
translating what you'd type into the address bar of the web browser. Domain names such as "google.com", into an 
[IP address](https://en.wikipedia.org/wiki/IP_address), like an ipv4 address "142.250.80.46" or an ipv6
address "2607:f8b0:4006:80b::200e". This "translating" service is called a DNS service  (DNS stands for [Domain Name System](https://en.wikipedia.org/wiki/Domain_Name_System)) 
Again, all the devices connecting to the internet are talking to a DNS server, which they were told how to find by the 
router, and the router was most likely told where to find the DNS server by the modem/ISP. Domain names are acquired from [domain name registrars](https://en.wikipedia.org/wiki/Domain_name_registrar).

## Connection

Long story short a wired connection provides the best performance and reliability but in reality it is not feasible to 
run wires everywhere. With more and more devices wanting access to the internet over Wi-Fi some discover that the 
signal across the home fades or slows. If the router doesn't provide a good enough signal throughout the home there are 
a couple options that could help improve the wireless connection quality throughout the home.  

At the funky farm one router wasn't enough to cover the property. The 1st option we tried here at the funky farm was 
using two existing routers, ran a new CAT6 cable to the opposite side of the property and installed the second 
router. The second router was configured to not "route" but instead act like a switch, but with Wi-Fi. This was an option 
provided by the router in the settings. That worked fine, aside from when going from one Wi-Fi to the other. Sometimes 
the devices would try to stay connected to the router that is further away, the signal would be just strong enough to 
not drop but would be super slow, or unresponsive until toggling the Wi-Fi on/off again to get it to connect to the 
closest router. 🤦‍♂️

#### NightHawk
To address the issue of having to toggle the Wi-Fi- on/off again & again we acquired a WiFi6 mesh kit with a router and 
two satellites by Netgear, the [Tri-band AX3600 3-Pack](https://www.netgear.com/home/wifi/mesh/mk83/). 
Our configuration had the nighthawk router wired to the existing home router and disabled the Wi-Fi on the existing home 
router. The 1st satellite talks to the nighthawk router, and the 2nd satellite talks the 1st satellite ( they talk on a 
hidden/unlisted connection ). This isn't ideal, as this topology could add latency, but devices sensitive to latency are 
connected with a wire. The connection was good and the transition between Wi-Fi radios was seamless. The thing that 
ultimately lead to the decision to stop using it was the lack of control and poor user experiencing interacting with the 
nighthawk's settings (through the mobile app).  

After setup, it began doing a "security" scan of every device connected to the network. Could not find the setting to 
change the DNS server in the configuration page and when using the custom DNS server address on the router that the 
nighthawk router connects to for internet, the devices connected to NighHawk couldn't access the internet. The custom 
DNS server blocks unwanted content & the nighthawk must be checking to see if it is online and the custom DNS server 
blocked the request. While it would be as easy as whitelisting the address in the DNS server, it was just another reason 
to look for a different solution.

#### Asus AiMesh
The [Asus AiMesh](https://www.asus.com/us/site/aimesh/) is not a particular device they sell but a technology built into 
the routers. Was previously using the [Asus AC1700 Gaming Router](https://www.asus.com/us/Networking-IoT-Servers/WiFi-Routers/ASUS-WiFi-Routers/RT-ACRH17/) 
router which is an older device, right before AIMesh was introduced. To achieve the mesh network had to upgrade the 
router and ended acquiring the [Asus AC1900 Gaming Router](https://www.asus.com/Networking-IoT-Servers/WiFi-Routers/ASUS-WiFi-Routers/RTAC68U/) 
which supports aiMesh and the [Asus RP-AC1900 Wi-fi Range Extender / AiMesh](https://www.asus.com/us/Networking-IoT-Servers/Range-Extenders-/All-series/RP-AC1900/). 
The range extender is connected to the router with CAT6 providing a fast and stable connection. Having used the previous 
generation of this router the setup was pretty straight forward and had the network back up in less than thirty minutes.

## Network Configuration 

A simple change that can be applied to most routers is the DNS configuration and as mentioned above this DNS service is 
used in nearly every network request. Depending on the goal there are a couple different solutions that could be setup.  

#### DNS
Just setting a known reliable DNS provider on the router can improve the performance and safety of the whole network.
With [OpenDNS](https://www.opendns.com/) as the DNS service you can get a simple solution to provide safe browsing for 
any device connected to the router by using the [family shield](https://www.opendns.com/setupguide/#familyshield) that, 
attempts to block adult content as well as setting custom parental controls.

To take it further and squeeze out a bit more performance and security we can run a service locally called [pi-hole](https://pi-hole.net/), 
which is a [DNS sinkhole](https://en.wikipedia.org/wiki/DNS_Sinkhole) and tell the router to use it for the DNS requests. 
What pi-hole does is handle all the DNS requests and for every request and checks black lists and white lists 
to determine if the request (domain) should be blocked. Pi-Hole still has to reach out to a public DNS 
server to fetch the address for good requests, but caches the queries which speeds up the feel of everyday browsing. 
To get the most out of pi-hole you'll want to choose a black list maintained by the community, these lists have the 
addresses of known ad servers and potentially dangerous servers from known sources.  

After years of configuring each device with ad blocking was happy to come across pi-hole and started using it 
immediately after discovering it. This has been a personal favorite option for ad blocking as it happens to any device 
connected to the network, and while it's not perfect, it's definitely worth the effort of setting it up. The screenshot 
below of the dashboard is showing it has blocked almost half of the requests made in the last 24hr span, but every 
device on the network is working fine. 🤓  

{{< figure src="/images/piHole24HR.PNG" title="Pi-Hole 24hr Stats" >}}
