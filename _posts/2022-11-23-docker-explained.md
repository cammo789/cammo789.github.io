---
title: Docker Compose Explained
date: 2022-11-23 15:30:00 -500
categories: [homelab, containers, docker, docker-compose]
tags: [homelab, containers, docker, docker-compose, iac]     # TAG names should always be lowercase
img_path: /img/
---

Ah, Docker Compose

![Docker Compose Logo](docker-compose-logo.jpg)

Compose is my first foray into [Infrastructure as Code](https://www.redhat.com/en/topics/automation/what-is-infrastructure-as-code-iac) and it's turned me into a believer. In 2021, after finally getting Linuxserver's SWAG stood up (more in this post), most apps take less than 10 minutes to set up and deploy with Compose. It's amazing and oh so easy. This makes me look forward to messing with Ansible and Terraform at some point.

In this and other posts, I'll apps, applications, and containers interchangeably.

#### Let's get into it

```yml
  sonarr:
    image: linuxserver/sonarr
    container_name: sonarr
    volumes:
      - /mnt/storage/sonarr/config:/config
      - /mnt/storage/tv:/tv
      - /mnt/disk1/downloads:/downloads
    ports:
      - 8989:8989
    restart: always
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
```

The above block is my yaml (pronounced yea-muhl) entry for [Sonarr](https://www.rapidseedbox.com/blog/ultimate-guide-to-sonarr)

```yml
image: linuxserver/sonarr
```
The 'image' defines the repository location of the container. This includes all the libraries needed to build it. You can think of this like a path or URL.

```yml
container_name: sonarr
```
I think this is self-explanatory. One thing to note is you can have different multiple instances of the same container all pulling from a single image. For example: I want one password manager for work and another for home. I would set something like this:

```yml
    image: vaultwarden/server:latest
    container_name: vault-work

    image: vaultwarden/server:latest
    container_name: vault-home
```

### Continuing,

```yml
    volumes:
      - /mnt/storage/sonarr/config:/config
      - /mnt/storage/tv:/tv
      - /mnt/disk1/downloads:/downloads
```
These are the locations that the container has access to. These and only these. This sandboxing serves as a convenient security feature built into Compose - processes can't accidently take over the host system.

One more thing of note is the ':' in each listing. To the left of it defines where in the **host** directory to create the volume. To the right of it defines where in the **container** directory to create the volume. Typically, you don't change the right side container locations, as the app typically looks for config files in set locations. You should only change the values to the left of the colon to suit your purposes


```bash
docker-compose up -d
```