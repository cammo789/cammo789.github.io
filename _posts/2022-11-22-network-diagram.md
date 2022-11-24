---
title: Network Diagram
date: 2022-11-22 15:30:00 -500
categories: [homelab, network, diagram, netgear]
tags: [network, diagram, netgear, mesh, pfsense, hp290]     # TAG names should always be lowercase
img_path: /img/
---

## Here's Our Current Network
![Network-Diagram-2022](netdiag_20221122.jpg)
_Your standard home network?_

As you can see, everything is tied to the Netgear mesh router, which consists of one main unit and two satellite access points ([APs](https://www.linksys.com/what-is-a-wifi-access-point.html)). The satellite units help with coverage on the property, but since it's still all one network, things will start to become limited if there are any high-bandwidth apps/streaming/etc. Additional satellite APs can be added later to further extend coverage. 

I wanted to get this documented, because today I scored my future [pfsense](https://en.wikipedia.org/wiki/PfSense) hardware, a [HP 290-p0043w](https://forums.serverbuilds.net/t/official-hp-290-p0043w-owners-thread/2829) for $100. That device will allow me to properly build out the home network with VLANs, firewalls, and a bunch of other features that can easily rival Ubiquiti's Dream Machine at a fraction of the price. I'll be learning more about the software soon, I just know I need to better carve out the home network if I want to have things like tons of wifi-enabled sensors, with security cameras, streaming gaming, all running smoothly.

You'll also probably notice that long list of applications on the left (under the NAS). I'll detail those more in another post.

## Future Network

![HP-290-glowing](hp290_glow.png)
_pfsense: The Network Savior?_