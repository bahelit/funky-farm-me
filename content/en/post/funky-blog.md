+++
date = 2022-04-11T11:14:48-04:00
description = "How this site was created & gets updated."
featured_image = '/images/logo.png'
tags = ["open source", "GoLang", "Hugo", "github"]
title = "Funky Blog"
+++

# Funky Blog ☁️

How this site was built, deployed and how it gets updated.  
<!--more-->

The Funky Farm blog is a static website, the website is generated ahead of time in contrast to dynamic websites where 
a web application builds the page on the fly based on various inputs. The majority of websites out there are dynamic 
websites such as google, amazon, twitter and other blogs like ones built on 
WordPress or Medium. They all gather data from some sort of database based on inputs like who is looking at the content to display a 
different looking page on the same web address. For example when two different users go to the web address twitter.com both 
see a completely different page based on whom they follow. Dynamic websites require a good bit of processing power from 
many systems communicating back and forth to each other before the page ready to be displayed to user.  

## Hugo
This static website is built using a tool called [Hugo](https://gohugo.io/) which takes human friendly files and 
generates a website from those files. In technical terms, Hugo takes a source directory of files and templates and uses 
these as input to create a complete website.  

#### Why Hugo
Hugo being written in GoLang was one primary reason as am personally quite fond of the go programming language. Hugo is 
extremely fast, from getting started from scratch to making changes and deploying. There's no worrying about setting up 
complicated runtimes, operating system dependencies or databases. Probably the best features is using a familiar text 
editor instead of a browser based text editor, this site is written using [GoLand](https://www.jetbrains.com/go/).  

{{< figure src="/images/posts/goLandHugo.PNG" title="Hugo in GoLand" >}}  

#### Install Hugo
Hugo can be installed on macOS, Windows, Linux, OpenBSD, FreeBSD, and on any machine where the Go compiler tool chain 
can run. See the official documentation for the various ways to [Install Hugo](https://gohugo.io/getting-started/installing/) 
or download it from the [Hugo Release](https://github.com/gohugoio/hugo/releases) page.

## Github
[Github](https://github.com/) is a place to share source code and is where this site is actually lives, it is a code 
repository at [https://github.com/bahelit/funky-farm-me](https://github.com/bahelit/funky-farm-me). Though this is not 
the actual website it is the source code that Hugo uses to generate the website that is published to GitHub. Anyone who 
checks out the source code can run the site locally on their PC with
{{< highlight bash >}}
hugo serve
{{< / highlight >}}


## Cloudflare
Cloudflare is an American content delivery network, they don't host website but provide services that make them faster. 
This website uses [Cloudflare Pages](https://pages.cloudflare.com/) to pull the website source code from GitHub which 
then generates the website with Hugo and make it available on its content delivery network. Did experience an issue at 
first with this, the version of Hugo that Cloudflare Pages uses is quite old and the site didn't appear correctly until 
setting it to use a newer version by setting the environment variable HUGO_VERSION to a recent release version.

## The Flow
The workflow process for maintaining this blog is pretty simple. Work on edits or new posts locally on my PC even while 
being offline. When the changes look good and are ready to go a keyboard shortcut pushes the changes to GitHub, after 
the changes have made it to GitHub Cloudflare detects and pulls those changes and rebuilds the static site with Hugo. 
This happens in a matter of seconds from a single button press from my machine.  
