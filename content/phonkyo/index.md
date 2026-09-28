---
title: Phonkyo
date: 2024-11-01
layout: product
build:
  publishResources: false
summary: A Raspberry Pi HAT that emulates an Onkyo-compatible dock.
description: >-
  Phonkyo is a pHAT for the Raspberry Pi that emulates an Onkyo RI dock and has
  a PCM5102A DAC. Stream Spotify, AirPlay or Plexamp to your Pi, and it can
  switch the receiver on and over to the dock input.
version: v0.3
price: €30
# The receiver display in the hero. Its bottom row links to sections of the page.
display:
  note: >-
    Plays Spotify, AirPlay and Plexamp, and switches the receiver on and over to
    its DOCK input when the music starts, and off again when it stops, once
    you've installed the software.
  links:
    - label: How it works
      href: "#how-it-works"
    - label: Board
      href: "#on-the-board"
    - label: Receivers
      href: "#receiver-compatibility"
    - label: Order
      href: "#ordering"
kits:
  - name: Basic kit
    price: €30 + shipping
    available: true
    contents:
      - Assembled Phonkyo board
      - 40-pin GPIO header, already soldered
  - name: Complete kit
    price: Not available yet
    available: false
    contents:
      - Assembled Phonkyo board
      - 40-pin GPIO header, already soldered
      - 3.5 mm to stereo RCA cable for audio
      - 3.5 mm to 3.5 mm cable for RI
      - 3D-printed case for a Raspberry Pi Zero 2 W with Phonkyo on top
# Receivers tested so far. works: turn on, turn off, dock input, TV input, volume,
# remote buttons.
receivers:
  - model: Onkyo TX-8020
    works: [true, true, true, false, false, true]
# Footnotes on the compatibility table, keyed by column name.
compat_notes:
  Volume: >-
    Volume here means changing the receiver's volume over RI. Software volume on
    the Pi always works, but it can only go as loud as the volume set on the
    receiver.
  Remote buttons: >-
    The receiver's own remote controlling playback through Phonkyo: play/pause,
    next and previous track, fast-forward, rewind and repeat. This works with
    Plexamp only.
---

## How it works

Onkyo receivers have a small 3.5 mm jack on the back labelled RI (Remote
Interactive). It's how an Onkyo dock tells the receiver to switch on and change
to the dock's input. Phonkyo speaks the same language, so to your receiver a
Raspberry Pi looks like a dock.

{{< hookup >}}

1. You play something on the Pi: Spotify from your phone (it shows up as a
   Spotify Connect speaker, using raspotify), AirPlay 2 from an iPhone, iPad or
   Mac (using shairport-sync), or your Plex library through Plexamp running
   headless.
2. Phonkyo sends the receiver a dock's commands over RI: switch on, change to
   the DOCK input.
3. The music comes out of Phonkyo's DAC and into that input.
4. After five minutes of silence, it switches the receiver off again, but only
   if it was the one that switched it on.


The switching is done by `phonkyo-monitor`, a small service that watches the
sound card. There's no one-step installer yet: the
[setup guide](/phonkyo/setup/) walks through installing it with the rest of the
software. It's tested on a Raspberry Pi Zero 2 W running Raspberry Pi OS Lite
(64-bit, Trixie).

### Your receiver's remote

With the receiver on DOCK, it passes the transport buttons of its own remote on
to the dock. Phonkyo listens for them, so the remote that came with your
receiver controls Plexamp:

- **Play/pause**, **next** and **previous track**
- **Fast-forward** and **rewind**, 10 seconds per press, and they keep going
  while you hold the button
- **Repeat**, cycling through off, repeat all and repeat one

This only works with Plexamp. AirPlay doesn't let the receiving end control the
phone that's sending, and the Spotify player on the Pi can't be controlled
locally, so for those, use your phone. Shuffle and Menu don't do anything yet.

## On the board

{{< figure-board >}}

- **Remote**: a 3.5 mm jack for the RI bus, with a series resistor and an ESD
  clamp between the jack and the Pi.
- **Line out**: a 3.5 mm stereo jack driven by a TI PCM5102A DAC over I²S. It
  is the same DAC chip used by the pHAT DAC and HiFiBerry DAC, so it works with
  their drivers.
- **ID EEPROM**: the board tells Raspberry Pi OS what it is, so the sound card
  comes up without editing `config.txt`.
- **pHAT size**: 65 × 30 mm, the footprint of a Pi Zero. It fits any Raspberry
  Pi with a 40-pin header.

## Kits

{{< kits >}}

Shipping is to European Union countries only.

## Receiver compatibility

Phonkyo should work with any receiver that has an RI jack and a DOCK input, but
RI support varies from one model to the next. Check that the features you need
work with yours before ordering.

{{< compat >}}

This is the only receiver tested so far. If you have a different RI receiver,
let me know what works and I'll add it here.

## Setup

Phonkyo needs Raspberry Pi OS Lite (64-bit) on the Pi, plus the software for
the sound card, the players you want and the receiver control. There's no
one-step installer yet, so it's done by hand, one command at a time. The guide
covers every step, from a blank microSD card to a receiver that switches itself
on.

<p><a class="button button-quiet" href="/phonkyo/setup/">Open the setup guide</a></p>

## Design files

The schematic, board layout and the software for the Pi are all public in the
[phonkyo repository on GitHub](https://github.com/fabiomsouto/phonkyo), under a
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) licence.
You can study them, change them and build your own board, as long as it isn't
for commercial use. If you share a modified version, it has to use the same
licence.

## Ordering

{{< order >}}
