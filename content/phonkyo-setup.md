---
title: Setting up Phonkyo
url: /phonkyo/setup/
layout: guide
summary: >-
  From a blank microSD card to a receiver that switches itself on when the
  music starts.
description: >-
  Step-by-step software setup for Phonkyo on a Raspberry Pi Zero 2 W: the sound
  card, Spotify Connect, AirPlay 2, Plexamp and the service that switches your
  receiver on and off.
---

There's no one-step installer yet, so this takes a while. Most of it is typing
commands into a terminal on the Pi. The steps follow the install notes in the
[phonkyo repository](https://github.com/fabiomsouto/phonkyo/blob/main/install/MANIFEST.md),
which also explain the reasons behind each one.

Everything here is tested on a Raspberry Pi Zero 2 W running Raspberry Pi OS
Lite (64-bit, Trixie). Spotify, AirPlay and Plexamp are each optional: skip the
ones you don't use.

## What you need

- A Raspberry Pi Zero 2 W, a microSD card and a power supply. The 64-bit
  system doesn't run on the original Pi Zero or Zero W.
- A Phonkyo board, with its 40-pin header soldered on.
- A 3.5 mm to stereo RCA cable for the sound, and a 3.5 mm to 3.5 mm cable for
  RI.
- A computer on the same network, to write the card and log in to the Pi.

## Write the SD card

Use [Raspberry Pi Imager](https://www.raspberrypi.com/software/). Choose the
Raspberry Pi Zero 2 W, then Raspberry Pi OS Lite (64-bit). Before writing, open
the settings and set:

- the hostname to `phonkyo`
- a username and password
- your Wi-Fi network
- SSH turned on

On Trixie these settings are applied on first boot by cloud-init. If you'd
rather write the `user-data` and `network-config` files yourself, the install
notes describe them.

## Connect the board

With the Pi unplugged, press Phonkyo onto the 40-pin header. Then:

- **Audio** jack to an analogue input on the receiver: the one it uses for the
  dock.
- **Remote** jack to the receiver's **RI** jack.

Power the Pi on and give it a minute or two on the first boot. Then log in from
your computer, with the username you chose:

```sh
ssh you@phonkyo.local
```

## Turn on the sound card

Open the boot configuration:

```sh
sudo nano /boot/firmware/config.txt
```

Turn off the Pi's own audio and HDMI audio, so Phonkyo is the first sound card.
The service that switches the receiver watches the first card, so this step is
needed on every board. Comment out the `dtparam=audio=on` line and add
`,noaudio` to the `vc4-kms-v3d` line:

```ini
#dtparam=audio=on
dtoverlay=vc4-kms-v3d,noaudio
```

Save, reboot with `sudo reboot`, log in again and list the sound cards:

```sh
aplay -l
```

You should see `card 0: sndrpihifiberry`. A v0.3 board loads its driver by
itself from its ID chip. If the card isn't there (for example on an older
board), add this line at the end of `config.txt`, under `[all]`, and reboot
again:

```ini
dtoverlay=hifiberry-dac
```

## Install the basics

```sh
sudo apt-get update
sudo apt-get install -y git python3-lgpio gpiod python3-gpiozero avahi-utils
```

`python3-lgpio` is what drives the RI jack. `avahi-utils` isn't strictly needed,
but it gives you `avahi-browse` for checking that AirPlay and Spotify are
visible on the network.

## Spotify Connect

Spotify Connect comes from raspotify, which has its own package source:

```sh
curl -sSL https://dtcooper.github.io/raspotify/key.asc \
  | sudo tee /usr/share/keyrings/raspotify_key.asc >/dev/null
echo "deb [signed-by=/usr/share/keyrings/raspotify_key.asc] https://dtcooper.github.io/raspotify raspotify main" \
  | sudo tee /etc/apt/sources.list.d/raspotify.list >/dev/null
sudo apt-get update && sudo apt-get install -y raspotify
```

It starts by itself and needs no configuration. Open Spotify on your phone and
the Pi appears as a speaker.

## AirPlay 2

Raspberry Pi OS only packages the older AirPlay, so AirPlay 2 is built from
source. That takes a while on a Zero 2 W. First the build tools:

```sh
sudo apt-get install -y build-essential autoconf automake libtool \
  libpopt-dev libconfig-dev libasound2-dev \
  avahi-daemon libavahi-client-dev libssl-dev libsoxr-dev \
  libplist-dev libplist-utils libsodium-dev \
  libavutil-dev libavcodec-dev libavformat-dev \
  uuid-dev libgcrypt-dev xxd
```

Then nqptp, the timing helper AirPlay 2 needs, and shairport-sync itself:

```sh
git clone --depth 1 https://github.com/mikebrady/nqptp.git
cd nqptp && autoreconf -fi && ./configure --with-systemd-startup \
  && make -j2 && sudo make install && cd ..

git clone --depth 1 https://github.com/mikebrady/shairport-sync.git
cd shairport-sync && autoreconf -fi && ./configure \
    --sysconfdir=/etc --with-alsa --with-soxr --with-avahi \
    --with-ssl=openssl --with-systemd --with-airplay-2 \
  && make -j2 && sudo make install && cd ..
```

Keep `-j2`: the Zero 2 W has 512 MB of memory, and more parallel jobs can run it
out.

Open `/etc/shairport-sync.conf` and set these two lines, removing the `//` in
front of them. This names the speaker and points it at Phonkyo's sound card by
name rather than by number:

```
name = "phonkyo";
output_device = "hw:CARD=sndrpihifiberry";
```

Then start both services and have them start at boot:

```sh
sudo systemctl enable --now nqptp shairport-sync
```

## Plexamp

Plexamp runs on Node.js, which Raspberry Pi OS packages:

```sh
sudo apt-get install -y nodejs
curl -sSL -o /tmp/plexamp.tar.bz2 \
  https://plexamp.plex.tv/headless/Plexamp-Linux-headless-v4.13.2.tar.bz2
sudo tar -xjf /tmp/plexamp.tar.bz2 -C /opt
sudo chown -R "$USER":"$USER" /opt/plexamp
```

The first run links the player to your Plex account. Get a claim token from
[plex.tv/claim](https://www.plex.tv/claim/), then run:

```sh
cd /opt/plexamp && node js/index.js
```

Paste the token, then give the player a name. The token only works once, and
it's used up even if the next prompt fails. If something goes wrong, get a new
one. When it says it's signed in and ready, wait a few seconds and stop it
with Ctrl+C.

Plexamp ships a service file written for a user called `pi` in
`/home/pi/plexamp`. Open `/opt/plexamp/plexamp.service`, change `User=pi` to
your username and every `/home/pi/plexamp` to `/opt/plexamp`, then install it:

```sh
sudo cp /opt/plexamp/plexamp.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable --now plexamp
```

## Receiver control

This is the part that makes the Pi act like a dock. `phonkyo-monitor` watches
the sound card. When music starts, it switches the receiver on and over to
DOCK. After five minutes of silence it switches the receiver off again, but
only if it was the one that switched it on. If you turned the receiver on
yourself for the TV or a record, it leaves it alone.

Install it from the phonkyo repository, as its own system user:

```sh
git clone --depth 1 https://github.com/fabiomsouto/phonkyo.git
sudo useradd --system --no-create-home --user-group --groups gpio,audio phonkyo
sudo mkdir -p /opt/phonkyo
sudo cp -r phonkyo/software/phonkyo /opt/phonkyo/
sudo cp phonkyo/software/systemd/phonkyo-monitor.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable --now phonkyo-monitor
```

To see it work, follow its log and play something:

```sh
journalctl -u phonkyo-monitor -f
```

## Check everything

```sh
systemctl is-active raspotify nqptp shairport-sync plexamp phonkyo-monitor
```

Each service you installed should say `active`. None of the players holds the
sound card while idle, so they can share it: whichever one starts playing gets
the sound.

If the Pi doesn't show up in AirPlay or Spotify, `avahi-browse -a` lists what
your network can see. If a player shows up but there's no sound, check
`aplay -l` again and make sure the receiver is on its DOCK input. The
[install notes](https://github.com/fabiomsouto/phonkyo/blob/main/install/MANIFEST.md)
cover more of what can go wrong, and why.
