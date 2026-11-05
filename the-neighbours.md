# The Neighbours

Xastir is one client among several, and the
map looks much the same from all of them —
the protocols are shared; the temperaments
differ. This chapter places the neighbours
the reader will meet, and points at the two
sibling guides that own the layers above and
below this one. None of the programs here
was installed in the lab; they are described
from their projects' documentation, in one
honest paragraph each, and are not ranked.

## The modem downstairs

**Dire Wolf** is not a neighbour so much as
the other half of the house: the software
TNC that turns a radio and a sound card into
a packet station, and the program Xastir
most often sits on top of via the AGW door
of chapter 5. Its guide in this series —
[Dire Wolf for Mere Mortals](https://paulsullivan33-dev.github.io/dire-wolf-for-mere-mortals/) —
covers AX.25 and APRS from the audio up,
including its own digipeater and igate, which
is why this guide sends you there for the
modem layer rather than repeating it. Note
the division of labour when both are running:
Dire Wolf owns the radio; Xastir owns the
map; a feature configured in both places at
once (digipeating is the classic) will happen
twice.

**Soundmodem and hardware TNCs** are the
other downstairs tenants: Soundmodem is the
other long-lived software modem (AGW-speaking,
hence also an Xastir door), and the hardware
TNC families named in Xastir's shipped
startup scripts — Kantronics, AEA, Kenwood's
built-ins — are the dedicated-hardware route,
configured by the scripts of chapter 5 rather
than by a second program.

## The other clients

**YAAC** — "Yet Another APRS Client" — is
the cross-platform Java client: the same map,
messages, and station memory, running
identically on Linux, Windows, and macOS,
which makes it the natural recommendation
when the station's computer is not a Linux
box. It speaks AGW and KISS to the same
modems Xastir does, so the two are
interchangeable at the interface and a matter
of taste at the desk.

**APRSIS32** is the Windows fixture of the
APRS world: a client built APRS-IS-first, at
home on the internet backbone, and widely
used for igates and event stations. If a
Windows machine must run the map, this is
usually why.

**PinPoint APRS** is the Windows tracker:
aimed at the moving station, with mapping
built around following vehicles and assets
rather than running a general APRS desk.

**APRSdroid** is the phone in the station:
an Android client that hears and (licensed)
beacons from a handset, with the phone's GPS
as the position source. It is the commonest
way a new operator first sees their own
track on a map — often on someone else's
Xastir.

## The view from the web

**aprs.fi** is the public web map of the
APRS-IS backbone — the place to see what the
internet side of the network currently holds,
station histories included, without running
anything. It is a service, not a client: it
cannot hear your local frequency, only what
igates have gated. When the local map and
aprs.fi disagree about a station, both are
telling the truth about different halves of
the system — the lab's specimen stations, of
course, exist on neither radio nor backbone,
but only in a file, which is precisely the
honesty the specimen was built for.

## The radio itself

Everything any client draws began as radio.
Licences, bands, antennas, and the conduct
of a station belong to
[Ham Radio for Mere Mortals](https://paulsullivan33-dev.github.io/ham-radio-for-mere-mortals/),
the series' foundation guide; this guide has
assumed its line between receiving and
transmitting throughout, and sends the reader
there to make the line their own.
