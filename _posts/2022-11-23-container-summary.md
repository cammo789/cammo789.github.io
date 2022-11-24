---
title: Homelab Containers Overview
date: 2022-11-23 15:30:00 -500
categories: [homelab, containers, docker]
tags: [homelab, containers, docker]     # TAG names should always be lowercase
img_path: /img/
---

## Remember This Monstrosity on the Network Diagram?
![Network-Diagram-2022](containers1.png)
_Let's dissect_

These are all applications currently running on the [NAS](https://en.wikipedia.org/wiki/Network-attached_storage). I figured yes, I could have had a storage device with a single purpose and run my apps on a separate device, but there is quite a bit of power in this old gaming rig - might as well put it to good use. 

More on the hardware and setup in another post.

## Let's dissect an app:

![Zoomed Container](container_zoomed.png)

### Starting on the top left:
1. Application name
2. The folder location of the application in the NAS
- The full path is /mnt/storage. So in this case: /mnt/storage/recipes/
3. The subdomain this app resides on
- In this case: recipes.mydomain.com

## As for the other symbols, from left to right

![Network Legend](network_legend.png)

1. I've dockerized everything on the NAS using [Docker Compose](https://docs.docker.com/compose/). Compose takes docker to the next level as it allows apps to be installed and deployed using just a few lines of code and with all the configuration (permissions, mount location, ports) in one text block. Any change to this block + refreshing the docker engine immediately puts those changes into effect. More on this in another post.

2. Simply, the app is a front-facing website on my domain.

3. Protected by [Authelia](https://www.authelia.com/), an open-source authentication and authorization server.

4. Protected with simple client-based authentication. It's not ideal. Authelia is the gold standard and what I'd prefer to protect all my apps, but for example some apps need to link up with other external apps. See [Sonarr](https://www.rapidseedbox.com/blog/ultimate-guide-to-sonarr) and [Lunasea (iOS)](https://www.lunasea.app/). Authelia will block them from talking to each other. There may be some advanced configuration within Authelia, but last I checked it's not supported. So for now I'm using simple username/password authentication. I really need to migrate these to something that at least has timeouts or X max retries to better protect my server from the web.

## Next up, how do all these apps get onto a domain with a valid SSL certificate?

## Enter Linuxserver's SWAG

![swag-gif](swag.gif)