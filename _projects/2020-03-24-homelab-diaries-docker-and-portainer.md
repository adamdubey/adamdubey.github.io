---
layout: single
author_profile: true
title: "Homelab Diaries: Docker & Portainer"
---

Getting up and running with Docker and Portainer in the homelab.

# Existing Infrastructure

I’ve recently expanded the actual lab portion of my homelab with another spec-stacked Dell R710, so it quickly got a fresh copy ESXi and added it to the cluster.

Now with fresh hardware up and running, it’s time to get Portainer setup and ready for use!

## Portainer & Docker: A cursory overview

Docker is typically described as _“Enterprise Container Platform for High-Velocity Innovation”_ and that about sums it up pretty nicely...kinda. I think folks get hung up on some of the deep technical aspects which adds fuzz to the basic understanding, but basically Docker containers provide a standardized environment for your applications to live in. There are numerous ways to configure your container, such as software and operating systems, however all of the containers are sharing the same host hardware, and most importantly the kernel.

Portainer is simply just a management UI to manage Docker environments. I tend to live in the CLI myself, but sometimes GUIs are nice too.

So Portainer isn’t exactly necessary for my needs, I still want to have it in the lab, even if it’s just for practicing and honing skills.

## Installing the Docker Host VM

For my Docker Host VM, I’m going with Photon OS. If you haven’t used it yet within your homelab, definitely give it a go! It’s really lightweight, and pretty seamless getting an instance running in VSphere since there are both OVA and ISO files.

Follow the process to get the Photon OS VM created per your environment, and perform the setup steps such as changing your password.

Next, we will need to configure Docker, which couldn’t be any easier with PhotonOS - Just enter these two commands:

```sh
$ systemctl start docker
$ systemctl enable docker
```

## Configuring Portainer

Just a few more commands to go before we’re done...So back at the Photon console:

```sh
$ docker volume create portainer_data
$ docker run -d -p 9000:9000 -name Portainer -restart always -v /var/run/docker.sock:/var/run docker.sock -v portainer_data:/data portainer/portainer
```

First we create the volume external to any container named `portainer_data`. Next, we install Portainer and configure it to listen on port 9000 with an additional flag to always restart in the event the container stops. Pretty painless eh?

You can open Portainer in your web browser of choice, by navigating to your instance’s IP address followed by the port number, for example:

`192.168.3.27:9000`

And that’s it! Just follow whatever wizards lurk ahead _(stuff changes all the time, and whatever I write will probably be obsolete soon)_.

## Next Steps

Thanks for sticking around! If you've followed to this point, the next steps you'd take would be to create project containers as necessary. There are way more features and aspects of each piece of tech I’ve elected to use here, but I feel this gets the practical hands-on approach for those of you playing along at home.
