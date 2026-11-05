# Xastir for Mere Mortals

APRS — the Automatic Packet Reporting System —
is amateur radio's habit of broadcasting small,
structured facts: where a station is, how fast
it is moving, what the weather is doing, a short
message for one other station. Those broadcasts
are only half a system until something collects
them and draws the picture. **Xastir** is that
something on Linux: a program that listens to
APRS traffic — from a radio through a TNC, from
a software modem, or from the APRS internet
backbone — and keeps a living map of every
station it has heard, with tracks, weather,
messages, and a memory of who said what, by
which path, and when.

Xastir is old software in the good sense. It
has been refined for over two decades, it is
unfashionably direct about what it is doing,
and its menus name real mechanisms instead of
hiding them: interfaces, paths, logs, filters.
This guide takes it on those terms — what each
part is for, what the map is actually telling
you, where the limits are, and what to check
when the map stays empty.

The lab is nine packets and no radio. The nine
packets are a specimen log file of invented
APRS traffic — a home station, a digipeater, a
moving car, a weather station, an object, a
message and its acknowledgement — which chapter
8 plays back into Xastir through its own
*Open Log File* feature while the station
counter, the map labels, and the station list
watch it happen. The build machine had no
radio, no TNC, and no GPS, and nothing in this
guide pretends otherwise: every workflow that
needs the air is marked as documented-only,
from Xastir's own bundled help, and
`criteria.md` keeps the full ledger.

A note on how this guide was verified. Xastir
2.2.0 (Ubuntu package 2.2.0-1build4) was
installed on Ubuntu 24.04 and run under a
virtual display: the first-run configuration
dialogue, the menus, the default configuration
file, and the complete decode of the specimen
log — six stations in the list, symbols,
paths, PHG, weather converted and displayed —
are captures, kept in `xastir-lab/transcripts/`.

## What this guide covers

- [**What APRS and Xastir are**](what-aprs-and-xastir-are.md) —
  the broadcast system, the client that draws
  it, the pieces of a station, and the line
  between receiving (open to all) and
  transmitting (licensed)
- [**Installing Xastir**](installing-xastir.md) —
  the Ubuntu package and what it brings with
  it, the first-run directory tree, and the
  version check
- [**First run and station setup**](first-run-and-station-setup.md) —
  the configuration dialogue that greets you,
  callsign and position, symbols and PHG, and
  the plain-text config file underneath
- [**Maps**](maps.md) — the built-in world map,
  the map types this build supports, online
  tile maps and their cache, and working
  offline
- [**Interfaces**](interfaces.md) — every way
  traffic reaches Xastir: serial TNC, KISS,
  AX.25, AGWPE, GPS, weather stations, and the
  APRS-IS internet feed
- [**Reading the map**](reading-the-map.md) —
  the specimen log decoded line by line:
  symbols, tracks, weather readouts, paths,
  and the station list as the station's memory
- [**Messaging and bulletins**](messaging-and-bulletins.md) —
  APRS messages and their acknowledgements,
  group messages, bulletins, and the message
  desk's machinery
- [**Logging and playback**](logging-and-playback.md) —
  the five logs, what a log file really is, and
  the verified playback of the specimen log
- [**The igate and digipeater question**](igate-and-digipeater.md) —
  what changes when your station stops only
  listening: gateway and relay duties, and the
  responsibilities that come with them
- [**The neighbours**](the-neighbours.md) —
  YAAC, APRSIS32, PinPoint, aprs.fi, and the
  modem side of the station in the sibling
  *Dire Wolf* guide
- [**Troubleshooting**](troubleshooting.md) —
  the placeholder callsign that will not go
  away, the station in the ocean, the empty
  map, and the log that will not play
- [**Glossary**](glossary.md) — the terms,
  collected in one place

## What it doesn't cover

The modem itself. Turning radio audio into
packets — Dire Wolf, hardware TNCs, levels and
wiring — is the sibling guide,
[Dire Wolf for Mere Mortals](https://paulsullivan33-dev.github.io/dire-wolf-for-mere-mortals/),
and the radio side of the hobby (licensing,
bands, antennas) lives in
[Ham Radio for Mere Mortals](https://paulsullivan33-dev.github.io/ham-radio-for-mere-mortals/).
APRS theory beyond what a map reader needs —
balloon and satellite work, telemetry formats
in depth, network design — is named where it
belongs and not taught. And nothing here will
help you transmit without a licence: receiving
is open to everyone, and this guide's lab is
entirely receive-side.

## How to use this guide

Read chapter 1, install with chapter 2, and
keep the specimen log
(`examples/specimen-log.txt`) nearby from
chapter 6 on — everything it contains is
decoded in the open, so you can check the
guide's reading of the map against the raw
packets yourself. When a radio joins the desk,
chapter 5 connects it, and nothing you learned
from the recording expires: the traffic is the
same, it is only live.
