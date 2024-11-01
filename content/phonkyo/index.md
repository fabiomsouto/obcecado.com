+++
title = 'Phonkyo'
date = 2024-11-01T00:45:29Z
draft = true
+++

# Phonkyo

Ever started watching your favorite show to realize your Onkyo amplifier is off, and your remote isn't
anywhere near you? I was you once, so I decided to do something about it!

This project started when I created a PiHat to expose controls for Onkyo's RI (Remote Interface) to
software, so I could use automations to turn on/off my amplifier. However, I've realized that wasting 
a Raspberry Pi Zero just to do this tiny task would be somewhat wasteful.

I wondered if I could also use the Raspberry Pi as a music player, and expose it as a Spotify Player, for example.
Turns out that, yes, it could be done!

I've then expanded the shield by also adding a DAC that's compatible with other DACs in the market, such as phatDAC
and Hifiberry.

Phonkyo (PiHat Onkyo) was therefore born!

## Description

This tiny DAC follows the footsteps of other market giants such as the phatDAC, by exposing a DAC that's capable of
reproducing high-quality audio, in a board that's designed with extra care to minimize noise or interference.
Beyond that, it also exposes a RI port, that allows control of Onkyo players with this port 
(the supported remote control features vary by amplifier, unfortunately, so make sure you confirm all the features you
need are available to your model, [here](#amplifier-compatibility)!).

## Features

- pHAT format board, compatible with 40-pin GPIO Raspberry Pi variants
- perfect match for Pi Zero's form factor
- 3.5mm female audio jack
- 3.5mm female RI jack
- PCM5102A DAC that works through Raspberry Pi's I2S interface

## Kits

There's two kits available for purchase.

### Kit 1 - Basic

This kit contains:

1. Assembled Phonkyo board
2. 2x20 0.1" female GPIO header (requires soldering)

I can also solder this header for you, free of cost; please add this request in the purchase notes if that's the case.

Price: 25EUR, plus shipping

Shipping to European Union countries.

### Kit 2 - Complete

This kit contains:

1. Assembled Phonkyo board
2. 2x20 0.1" female GPIO header, pre-soldered
3. 3.5mm male audio jack to RCA stereo connectors
4. 3.5mm male jack to 3.5mm male jack cable for RI

Price: Not available yet

## Software

The default software configuration is very similar to the likes of phatDAC or Hifiberry, since they're compatible.
However, there are interesting features besides this that I've wanted to have available:

- Exposing the device as a Spotify Connect device (using raspotify)
- Exposing the device as an Airplay device (using shairport)
- Exposing the device as a Plexamp headless player
- Exposing the RI interface for automation control

### Configuration

Please follow the guide here! Happy tunes!

## Amplifier RI features

The table below summarizes the supported RI features, by device model.

|               | Turn on | Turn off | Switch to Dock input | Switch to TV input | Volume control |
|---------------|---------|----------|----------------------|--------------------|----------------|
| Onkyo TX-8020 | Yes ❤️  | Yes ❤️  | Yes ❤️               | No 💔             | No 💔          |