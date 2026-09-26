---
title: Phonkyo
date: 2024-11-01
layout: product
build:
  publishResources: false
summary: A Raspberry Pi HAT that switches on your Onkyo amplifier and plays music through it.
description: >-
  Phonkyo is a pHAT for the Raspberry Pi with a PCM5102A DAC and an Onkyo RI
  remote port. Use your Pi as a Spotify Connect, AirPlay or Plexamp player
  that turns your amplifier on by itself.
version: v0.3
price: €30
# The tuner dial in the hero. One stop per thing the board does.
dial:
  - label: Remote
    text: Switches your Onkyo amplifier on and picks the input.
  - label: Spotify
    text: Shows up in the Spotify app as a Connect speaker.
  - label: AirPlay
    text: Takes AirPlay 2 streams from an iPhone, iPad or Mac.
  - label: Plexamp
    text: Plays your Plex music library as a headless player.
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
---

## Why it exists

Ever sat down to watch something, only to find the amplifier off and the remote
nowhere near you? Onkyo amplifiers have a small 3.5 mm jack on the back, labelled
RI (Remote Interactive), that other Onkyo gear uses to switch them on and change
inputs. Phonkyo gives that jack to a Raspberry Pi, so your home automation can do
it instead.

Using a whole Pi just to press a power button felt wasteful, so the board also
has a proper audio DAC. The same Pi that switches the amplifier on can be the
thing playing music into it.

## On the board

{{< figure-board >}}

- **Line out**: a 3.5 mm stereo jack driven by a TI PCM5102A DAC over I²S. It
  is the same DAC chip used by the pHAT DAC and HiFiBerry DAC, so it works with
  their drivers.
- **Remote**: a 3.5 mm jack for Onkyo's RI bus, with a series resistor and an
  ESD clamp between the jack and the Pi.
- **ID EEPROM**: the board tells Raspberry Pi OS what it is, so the sound card
  comes up without editing `config.txt`.
- **pHAT size**: 65 × 30 mm, the footprint of a Pi Zero. It fits any Raspberry
  Pi with a 40-pin header.

## What you can do with it

- Play Spotify through it as a Spotify Connect speaker (raspotify)
- Stream to it from an iPhone or Mac over AirPlay 2 (shairport-sync)
- Run it as a headless Plexamp player
- Switch the amplifier on and change its input from Home Assistant or a script
- Switch the amplifier on automatically when music starts playing

The software stack is tested on a Raspberry Pi Zero 2 W running Raspberry Pi OS
Lite (64-bit, Trixie). A step-by-step setup guide is coming. In the meantime,
guides written for the HiFiBerry DAC apply to the audio side.

## Kits

{{< kits >}}

Shipping is to European Union countries only.

## Amplifier compatibility

RI support varies from one amplifier to the next. Check that the features you
need work with your model before ordering.

| Model         | Turn on | Turn off | Dock input | TV input | Volume |
|---------------|---------|----------|------------|----------|--------|
| Onkyo TX-8020 | Yes     | Yes      | Yes        | No       | No     |

This is the only amplifier tested so far. If you have a different RI amplifier,
let me know what works and I'll add it here.

## Ordering

{{< order >}}
