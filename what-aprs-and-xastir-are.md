# What APRS and Xastir Are

## APRS in one paragraph

APRS, the Automatic Packet Reporting System,
is a way for amateur radio stations to
broadcast small, standardised facts about
themselves: a position, a course and speed, a
weather reading, a short status, a text
message addressed to one other station. The
broadcasts travel as AX.25 packets — on the
air, usually on 144.390 MHz in North America
— and any station in earshot can hear all of
them. There is no connection and no
conversation at the radio layer: a station
speaks its fact into the room, digipeaters
may repeat it once or twice so the room gets
bigger, and internet gateways may carry it
onto the APRS-IS backbone, where the whole
world's APRS traffic flows past anyone who
connects. The system was built by Bob
Bruninga, WB4APR, and its unit of meaning is
the single self-contained packet: hear one
packet, learn one fact.

## What Xastir is

Xastir — the name expands, in its own window
title, to *X Amateur Station Tracking and
Information Reporting* — is the program that
collects those facts and draws them. It is an
**APRS client**: it does not generate or
demodulate radio signals itself. It takes in
decoded packets from something else — a
hardware TNC, a software modem such as Dire
Wolf, a GPS, the internet — and maintains:

- **The map.** Every heard station, object,
  and weather report placed at its reported
  position, as a symbol, with its callsign.
- **The memory.** A station database behind
  the map: when each station was last heard,
  by what path, with what comment — the list
  in chapter 6.
- **The desk.** Tools for the interactive
  half of APRS: messages in and out,
  bulletins, objects of your own, queries to
  other stations.
- **The record.** Logs of everything heard,
  which can be played back later — the
  mechanism this guide's lab is built on
  (chapter 8).

The separation matters. When the map is
empty, the fault can live in the radio, the
modem, the cable, or the client, and Xastir
only owns the last of those. The sibling
guide, *Dire Wolf for Mere Mortals*, covers
the modem layer; this guide covers the
client layer and says plainly where the
boundary lies whenever it matters.

## A station, in pieces

A working Xastir station can be as small as
a laptop with an internet connection, or as
involved as a radio, a GPS, and a weather
station. The pieces, and which chapters own
them:

| Piece | Job | Chapter |
|---|---|---|
| Xastir | Map, memory, desk, record | This guide |
| TNC or software modem | Audio ⇄ packets | *Dire Wolf* guide |
| Radio | Puts packets on the air, hears them | *Ham Radio* guide |
| GPS | Tells your station where *it* is | Ch. 5 |
| Weather station | Feeds local weather reports | Ch. 5 |
| APRS-IS connection | The internet backbone, worldwide traffic | Ch. 5 |

## Receiving is open; transmitting is licensed

This is the safety and legality line for the
whole guide, stated once and plainly.

**Receiving APRS — on the air or from
APRS-IS — is open to anyone.** No licence is
needed to listen, to map what you hear, or to
play back recordings of it. Everything in
this guide's lab is receive-side.

**Transmitting APRS is amateur radio.** The
moment your station puts a packet on the air
— a beacon, a message, a digipeat, an
internet-to-RF gateway transmission — you are
transmitting in the amateur service and need
the licence, the callsign, and the habits
that go with them: identify with your real
callsign, use your own APRS-IS passcode and
nobody else's, and take responsibility for
what your station repeats. Xastir will let
you configure a station before it ever asks
whether you are licensed; the asking is your
job. Chapters 7 and 9 cover the transmitting
features with that duty attached, and the
lab never uses them.

One consequence worth knowing now: APRS is a
*public* system by design. Positions,
weather, and messages are broadcast in the
clear for anyone to hear and are archived by
public services. Never put anything in an
APRS packet — a comment, a message, an object
— that you would not read aloud in a room
full of strangers, because that is precisely
where you have said it.

## The lab

The build machine for this guide had Xastir
2.2.0, a virtual screen, and no radio, TNC,
or GPS. The lab is therefore one file:
`examples/specimen-log.txt`, nine lines of
invented APRS traffic in the raw form a TNC
would print it, every station a placeholder
and every location a round number near
40°N 75°W:

| Line | From | What it is |
|---|---|---|
| 1 | N0CALL-1 | A digipeater's position, with PHG |
| 2 | N0CALL | A home station's position |
| 3–4 | N0CALL-9 | A car, twice — a short track |
| 5 | N0CALL-2 | A weather report |
| 6 | N0CALL | An object: PICNIC |
| 7–8 | N0CALL-9 ⇄ N0CALL | A message, and its ack |
| 9 | N0CALL-9 | A status text |

N0CALL is the placeholder callsign APRS
software itself uses before you configure
one — nobody's call, chosen so nothing in the
lab is a real station. Chapter 6 reads each
line against what Xastir made of it, and
chapter 8 shows the playback itself.

Check: the specimen is plain text and readable
right now —

```text
N0CALL-9>APRS,WIDE1-1,WIDE2-1:!3959.80N/07459.50W>090/012/A=000450 Fictional mobile station
```

Read it as: station `N0CALL-9`, sending to
`APRS` by way of `WIDE1-1,WIDE2-1`, reports
(`!`) latitude 39°59.80′N, longitude
074°59.50′W, with a car symbol (`>`), moving
090° at 12 knots at 450 feet, and says so in
the comment. Every packet in APRS opens up
the same way once you know the shape.
