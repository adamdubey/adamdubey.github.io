---
layout: single
author_profile: true
title: "Flight tracking with PiAware"
---

_Surely you can't be serious..._

# Project Overview

Over the past few days I had been working on migrating a few services within my "Radio Lab" to containerized services, which freeded up both space on my desk as well as a few Raspberry Pi's, which was exactly what I needed to build a new PiAware ADS-B ground station!

The minimum bill of materials for this project are:

- Raspberry Pi (including power supply, micro sd card, etc to make RasPi work...)
- FlightAware Pro ADS-B Reciever
- MCX antenna plug with SMA adapter

There are several kits available out there, or you can piecemeal one together using the components of your choosing.

Additionally, before proceeding with the build let's roughly outline the project:

A.) Setup/Install/Build
B.) Testing and Usage
C.) Expansion

Pretty straight forward, so off to the workbench we go...

## Setup/Install/Build

To start, I'd advise following these instructions, and stopping after completing step 2:

[piaware](https://flightaware.com/adsb/piaware/build)

Once the Pi is booted up there are a few options, and the choice is up to you on how to administer the device,

## Usage

## Expansion

You now have a <> up and running! So what's next? Well that's entirely up to you, and how far you'd like to push the range of being able to intercept the adsb messages from aircraft. From my experience, I've been able to intercept up to a 40,000' flight level ceiling within a 15 mile radius using a nub antenna on ground level.

Also contengent is _how busy is air traffic in your area_? Currently due to COVID-19, the skies have been rather empty aside from cargo planes and a few occational 737/A320 & RJs. Additionally, if you are fortunate enough to live in an area with multiple airfields, you will have far more traffic lighting up your map than say being located next to an un-manned airfield that doesn't see much traffic on a regular basis.

## Livin' the dream!

The best recomendations I could give for expansion in general would be two things:

1. [Adding a signal line dampener]()
2. [Bigger Antenna]()

While the first item is something you'd need to aquire, the latter could actually be made with very basic materials - on the contrary you could also just stick with what you have and try to get it as high in elevation as possible, unobstructed within a 360 degree radius and a 5-foot minum to get a clearer signal from aircraft transponders.

_...and don't call me Shirley._
