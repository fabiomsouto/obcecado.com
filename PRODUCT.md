# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

People who own an Onkyo receiver, or another receiver with an RI (Remote
Interactive) jack, and want a Raspberry Pi streamer that behaves like an Onkyo
dock: it switches the receiver on, selects its input and plays music through it.
That includes Pi tinkerers, but also less technical owners who mainly want
"press play on my phone, the receiver comes on". They need to work out quickly whether it fits their receiver and
setup, what they get, and how to order.

## Product Purpose

obcecado.com is the personal site of Fabio Souto, a software developer, for
hardware made as a hobby. Right now it exists to present and sell Phonkyo, a
Raspberry Pi pHAT with a PCM5102A DAC and an Onkyo RI remote port. Success means
a visitor understands what Phonkyo does, can tell whether it will work with
their amplifier, and sends an order email.

More projects may or may not follow. The home page lists projects, but the site
should not present itself as a studio, shop or catalogue that it isn't.

## Positioning

Phonkyo is a dock emulator: to the receiver it looks like one of Onkyo's own
RI docks, so the receiver turns on and switches to the dock input by itself
when music starts. It pairs that with a proper line-level DAC on the same small
board, so the Pi that talks to the receiver is also the source playing into it.
General-purpose Pi DACs (pHAT DAC, HiFiBerry) cover only the audio; Phonkyo uses
the same DAC chip, so their drivers and guides still apply.

## Operating Context

- Hardware: any Raspberry Pi with a 40-pin header; tested on a Pi Zero 2 W with
  Raspberry Pi OS Lite (64-bit, Trixie).
- Software used with it: raspotify (Spotify Connect), shairport-sync
  (AirPlay 2), Plexamp headless.
- RI support varies by receiver; only the Onkyo TX-8020 is tested. Other
  receivers with an RI jack may work but are unconfirmed.
- Ordering is by email to `phonkyo@obcecado.com` (`params.orderEmail`); Fabio
  replies with the total including shipping and how to pay. No checkout.
- Shipping is to EU countries only.

## Capabilities and Constraints

- Static Hugo site with no theme; deployed to S3 behind CloudFront on push to
  `main`. Product data (kits, price, the hero dial) lives in the page's front
  matter.
- Phonkyo board: PCM5102A DAC over I²S to a 3.5 mm line out, 3.5 mm RI jack with
  series resistor and ESD clamp, ID EEPROM so the sound card needs no
  `config.txt` edits, pHAT size 65 × 30 mm. Current revision v0.3.
- Dock behaviour: the `phonkyo-monitor` service (in the phonkyo repo) watches
  the sound card, sends power on + DOCK when playback starts, and powers off
  after 5 minutes of silence, only if it powered the receiver on. The buyer
  installs it by hand, following the setup guide at /phonkyo/setup/; there is
  no one-step installer yet.
- Kits: Basic kit (assembled board, header soldered) is available; Complete
  kit (adds audio and RI cables) is not available yet.
- **Undecided:** the final price. €30 + shipping is on the page but is not
  final.
- Terminology: "RI", "pHAT", "kit". Keep technical terms accurate; explain them
  in plain words for the less technical visitor.

## Brand Commitments

- Name: obcecado (Portuguese for "obsessed"), domain obcecado.com. Product name:
  Phonkyo.
- Voice: first person, one maker speaking plainly and honestly about a hobby
  project. Small batches, built by hand. No corporate "we", no hype.

## Evidence on Hand

- Board renderings from the KiCad design: `content/phonkyo/board-iso.png`,
  `content/phonkyo/board-top.png`.
- One tested amplifier (Onkyo TX-8020) with its feature table.
- Setup guide: `content/phonkyo-setup.md` (/phonkyo/setup/), following
  `install/MANIFEST.md` in the phonkyo repo.
- Design files and software: the KiCad schematic and board, and the Pi software
  stack, are in https://github.com/fabiomsouto/phonkyo under CC BY-NC-SA 4.0
  (decided 2026-09-26). Name the licence rather than calling it "open source":
  the non-commercial clause means it isn't open source in the OSI sense.

Absent, and not to be fabricated: photos of physical boards, buyer counts,
testimonials or reviews, press, and additional tested amplifiers. Don't mention
Home Assistant or home automation, or claim a history of Onkyo iPod docks.

## Product Principles

1. Lead with the dock idea: the receiver wakes up and switches input on its own.
   Integrations are extras, not the pitch.
2. Honest over impressive: say what is tested, what isn't, and what isn't
   available yet.
3. Answer "will it work with my amp?" before asking for an order.
4. Make it approachable for the non-tinkerer without hiding the technical detail
   the tinkerer wants.
5. It's a hobby made by one person; the site should feel like that, not like a
   company.
