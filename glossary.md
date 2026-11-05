# Glossary

**Ack** — The acknowledgement packet for an
APRS message: a reply whose whole text is
`ack` plus the message's identifier. Senders
retry until it arrives.

**AGWPE** — A packet-engine protocol (and the
Windows program that defined it) by which
client programs talk to a modem over a
network connection. One of Dire Wolf's two
doors, and Xastir's "Networked AGWPE"
interface type.

**APRS** — Automatic Packet Reporting System:
amateur radio's broadcast system for
positions, weather, objects, and short
messages, built on AX.25 by Bob Bruninga,
WB4APR.

**APRS-IS** — The APRS Internet System: the
network of servers (the "backbone") that
carries the world's APRS traffic between
igates and internet-connected clients.

**AX.25** — The packet-radio link protocol
underneath APRS: frames between callsigns,
digipeater paths included.

**Beacon** — A station's periodic position or
status broadcast, sent whether or not anyone
asked.

**Bulletin** — An APRS message addressed to
everyone (`BLN…`), for area-wide information;
announcements are bulletins repeated on a
schedule.

**.dbfawk** — Xastir's styling rule files for
shapefile maps: which colours and lines each
kind of feature draws in.

**Digipeater** — A station that repeats
packets it hears so they travel further. Each
repetition costs a full transmission on a
shared channel.

**Filter (APRS-IS)** — A string sent to an
internet server narrowing the feed it
forwards: an area, a radius, named stations.

**GNIS** — The USGS Geographic Names
Information System; Xastir can plot and
search its place-name data.

**Igate** — Internet gateway: a station that
copies traffic between radio and APRS-IS, in
either or both directions, under a licensed
operator's responsibility.

**KISS** — "Keep It Simple, Stupid": the
framing by which a TNC moves raw AX.25 frames
and leaves the protocol to the computer.

**Mic-E** — A compressed position format,
originating in microphone-encoder radios,
that packs latitude into the packet's
address field. Xastir decodes it like any
other position.

**Object** — A map feature that is not a
station: a picnic, an incident, a finish
line, reported by a station on behalf of the
thing itself. Items are objects without
timestamps of their own in the same family.

**Passcode** — The APRS-IS password, computed
from a callsign by a public algorithm
(`callpass` computes it). Required before the
backbone accepts your traffic for relay.

**Path** — The digipeater route a packet asks
for or has taken: `WIDE1-1,WIDE2-1` and its
kin. The station list's Path column shows the
last packet's route.

**PHG** — Power, Height, Gain (and
directivity): four digits from which other
stations estimate a transmitter's coverage
circle.

**Posit** — A position report packet.

**RELAY digipeat** — Xastir's fill-in
digipeating: repeat when the path's first
unused alias is your callsign or one you
list. For demonstrable gaps only.

**SSID** — The number after a callsign's dash
(`-9`, `-1`), distinguishing a person's
stations: car, home, weather, digipeater.

**Symbol table / code** — The two characters
in a position packet that choose its map
icon: which table (`/` primary, `\`
alternate, or an overlay character) and which
picture in it.

**TNC** — Terminal node controller: the modem
between a radio and a computer, hardware or
(increasingly) software such as Dire Wolf.

**Track** — The line joining a mobile
station's successive positions on the map;
also the exported file of those positions,
which Open Log File will not read.

**Tracklog** — Xastir's saved station tracks
under `~/.xastir/tracklogs/`, in `.trk`, KML,
and shapefile forms. Exports, not recordings.

**WIDE / WIDEn-N** — The generic digipeater
aliases of the modern APRS network: `WIDE1-1`
for fill-in digipeaters, `WIDE2-1` and kin
for the wide-coverage machines.
