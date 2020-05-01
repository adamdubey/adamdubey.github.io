---
layout: single
author_profile: true
title: "Flight tracking with PiAware"
---

Surely you can't be serious...

# Livin' the dream!

![livin-the-dream](/assets/images/piaware/livin-the-dream.png)

Ever wonder exactly how fast or high that plane that just flew by was? Or though, _"Geeze, close call there skip"_...yeah no, no it wasn't a close call at all - but you wouldn't know that unless you had your own ground station monitoring the skies.

paragraph 2

Prerequisites:

- Raspberry Pi v2 or greater (Model Zero W can be used as well)
- 1090 MHz Antenna

paragraph 3

## Installation and setup

Starting out with getting the Raspberry Pi provisioned, it'll be a rather straightforward process. Buster or Noobs OS will be more than sufficient [tested with both, can't vouch for other distros]

During the initial OS configuration, be sure to enable SSH access - it'll come into play shortly!

[piaware](https://flightaware.com/adsb/piaware/install)

## Usage

## Expansion

You now have a <> up and running! So what's next? Well that's entirely up to you, and how far you'd like to push the range of being able to intercept the adsb messages from aircraft. From my experience, I've been able to intercept up to a 40,000' flight level ceiling within a 15 mile radius using a nub antenna on ground level.

Also contengent is _how busy is air traffic in your area_? Currently due to COVID-19, the skies have been rather empty aside from cargo planes and a few occational 737/A320 & RJs. Additionally, if you are fortunate enough to live in an area with multiple airfields, you will have far more traffic lighting up your map than say being located next to an un-manned airfield that doesn't see much traffic on a regular basis.

The best recomendations I could give for expansion in general would be two things:

1. [Adding a signal line dampener]()
2. [Bigger Antenna]()

While the first item is something you'd need to aquire, the latter could actually be made with very basic materials - on the contrary you could also just stick with what you have and try to get it as high in elevation as possible, unobstructed within a 360 degree radius within a 5-foot minum to get a clearer signal from aircraft transponders.

And if you don't care about tracking aircraft, well at the very least you now have a weather radar.

...and don't call me Shirley.
