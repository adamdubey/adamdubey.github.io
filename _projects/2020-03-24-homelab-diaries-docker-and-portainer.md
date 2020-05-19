---
layout: single
author_profile: true
title: "Homelab Diaries: Docker & Portainer"
---

Getting up and running with Docker and Portainer in the homelab.

# Portainer & Docker: A cursory overview

Docker is typically described as _“Enterprise Container Platform for High-Velocity Innovation”_ and that about sums it up pretty nicely...kinda. I think folks get hung up on some of the deep technical aspects which adds fuzz to the basic understanding, but basically Docker containers provide a standardized environment for your applications to live in. There are numerous ways to configure your container, such as software and operating systems, however all of the containers are sharing the same host hardware, and most importantly the kernel.

Portainer is simply just a management UI to manage Docker environments. I tend to live in the CLI myself, but sometimes GUIs are nice too, especially if you are managing multiple Docker environments.

Through several days of experimenting, multiple variations and approaches to administration and pushing the boundaries, I don't think Portainer really fits my particular workflows other than being useful for getting granular centralized telemetry data of my Docker containers.

So with that being said, here are my two best approaches to working with Portainer in your own labs...

## Option 1: Installing the Docker Host VM with Photon

For my lab stack, I’m going with Photon OS. If you haven’t used it yet within your homelab, definitely give it a go! It’s really lightweight, and pretty seamless getting an instance running in VSphere since there are both OVA and ISO files.

Follow the process to get the Photon OS VM created per your environment, and perform the setup steps such as changing your password.

Next, we will need to configure Docker, which couldn’t be any easier with PhotonOS - Just enter these two commands:

```sh
$ systemctl start docker
$ systemctl enable docker
```

In a grand total of 3 minutes, I now have a VM to muck up as much as I want with Docker experiments! Not a big deal if shit goes sideways, rollback to a snapshot or just rebuild the whole VM!

## Option 2: Install the Docker Host VM with Ubuntu

I have to admit that I like this option a little bit more than the prior, mainly because I don't have to context switch as much when it comes to managing the host OS. However, this approach does take a little more time (_even with automation_), but is totally worth it - especially if you remember to snapshot the VM before proceeding...Into the Production stack will go a fresh VM with the latest Ubuntu offering!

```sh
# Update system packages

$ sudo apt-get update
$ sudo apt-get upgrade

# Install Docker and enable service

$ sudo apt install docker.io
$ sudo systemctl start docker
$ sudo systemctl enable docker

# Fix Permissions to make Docker administration easier

$ sudo usermod -aG docker ${USER}
$ su - ${USER}
```

And just like that, a new VM is ready and awaiting...

## Configuring Portainer

Alright now it's time to make some big decisions, and it'll come down to answering this question:

_"How do I want to administer my Docker containers?"_

Typically I test out a new service in my Lab stack manually first, and then if it's a Production service, spin it up via Docker Compose.

Let's take a look at bringing up Portainer manually first:

```sh
$ docker container run -d \
 -p 9000:9000 \
 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer
```

And if we are going to build expressly for Production:

```yml
# docker-compose.yml

version: "3"
services:
  #####PORTAINER#####
  portainer:
    container_name: portainer
    image: portainer/portainer
    volumes:
      - portainer_data:/data
      - /var/run/docker.sock:/var/run/docker.sock
    restart: always
    ports:
      - "9000:9000"

#####VOLUMES#####
volumes:
  portainer_data:
```

To finish the install, you can open Portainer in your web browser of choice, by navigating to your instance’s IP address followed by the port number, for example:

`192.168.3.27:9000`

And that’s it! Just follow whatever wizards lurk ahead _(stuff changes all the time, and whatever I write will probably be obsolete soon)_.

## Next Steps

Now that the service is running, you can add whatever containers you want to be monitored by Portainer, just by spinning up a new service or adding to your existing docker-compose file and re-building.

As an example, here is my current Lab stack testing a TIG stack _(Telegraf, InfluxDB, Grafana)_ for centralized telemetry:

![portainer-dashboard](/assets/images/portainer/portainer-overview.png)

Just by having the Docker containers all running on the same host, Portainer is able to capture and display them in a single spot.

Happy experimenting!
