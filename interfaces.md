# Interfaces

An **interface** is one pipe between Xastir
and a source of packets. Interfaces are
managed in one place — **Interface →
Interface Control** — where each is added
from a type list, given properties, and told
whether to start when Xastir starts. A
station can run several at once: the classic
setup is a radio TNC and an internet
connection side by side, each feeding the
same map.

The verification line for this chapter, said
once: the lab had no TNC, no radio, no GPS,
and made no connection to APRS-IS, so no
interface here was started. What the lab
verified is the machinery around them — the
type list below is Xastir's own, from its
bundled help; the compiled-in support was
confirmed from the installed binary's
libraries (libax25 among them); and the
default interface record was read from the
configuration file. Behaviour of each type
is described from the bundled help, and the
chapter says so where it matters.

## The type list

Xastir's own list of supported interface
types, verbatim from its help:

```text
Serial TNC
Serial TNC w/GPS on HSP cable
Serial GPS
Serial WX
Internet Server
AX.25 TNC
Networked GPS (via gpsd)
Networked WX
Serial TNC w/GPS on AUX port
Serial KISS TNC
Networked Database (Not Implemented Yet)
Networked AGWPE
Serial Multi-Port KISS TNC
SQL Databases [MySQL,Postgis] (Experimental)
```

Grouped by what they connect:

## Radio doors: TNCs

A **TNC** (terminal node controller) is the
modem between radio audio and packet data.
Xastir speaks to them several ways:

- **Serial TNC** — a hardware TNC on a serial
  port, driven in its command mode. The
  package ships per-model startup and stop
  scripts in `/usr/share/xastir/config/`
  (`tnc-startup.kpc3`, `tnc-startup.d700`,
  `tnc-startup.thd7`, and a dozen siblings) —
  evidence of the era Xastir grew up in, when
  each TNC family wanted its own incantations.
  The properties for this type include the
  igate option and the RELAY digipeat switch
  of chapter 9.
- **Serial KISS TNC** — a TNC (or a software
  modem presenting as one) in KISS mode,
  where the device moves raw frames and
  Xastir does the protocol work. This is the
  commonest modern arrangement, and the
  *Serial Multi-Port KISS TNC* variant covers
  devices with several radio ports.
- **AX.25 TNC** — the Linux kernel's own
  AX.25 stack, with Xastir talking to kernel
  network devices. This build links libax25,
  so the option is real here; the kernel side
  (ports, `ax25d`, callsign assignment) is a
  subject of its own and belongs to the
  packet-radio literature, not this guide.

## The software-modem door: AGWPE

**Networked AGWPE** connects over the network
to an AGWPE-compatible packet engine — which
is one of the two doors **Dire Wolf** offers,
the sibling guide's chapter 7 being the full
account. This is how the lab's own fleet of
guides fits together: Dire Wolf listens to
the radio and speaks AGW; Xastir connects to
it as a client and draws the map. The bundled
help notes the AGW login convention (your
callsign, in capitals, as the username) for
engines with security enabled. KISS-over-TCP
to Dire Wolf's other door is the alternative
arrangement, reached through the KISS types
above via a serial-port emulator; the AGW
route needs no such plumbing and is the one
to reach for first.

## The internet door: APRS-IS

**Internet Server** is Xastir's name for an
APRS-IS connection: host, port, and the data
of the whole APRS world, filtered to what
you ask for. Its properties, from the bundled
help, are the ones that matter:

- **Activate on start up** and **Allow
  Transmitting** are separate switches —
  receiving and being allowed to send are
  different decisions, and Xastir keeps them
  so.
- **Passcode.** Your APRS-IS passcode is
  computed from your callsign by a public
  algorithm; the package ships the calculator:

  ```bash
  callpass N0CALL
  ```

  ```text
  Passcode for N0CALL is 13023
  ```

  Without a valid passcode your connection is
  receive-only in effect — the backbone will
  not accept your traffic for relay. Treat
  your own passcode as a password anyway: it
  is the only thing standing between the
  network and someone beaconing as you. Never
  use anyone else's callsign or passcode, and
  never connect with a callsign that is not
  yours.
- **Filter parameters.** A filter string sent
  to the server so it forwards only the slice
  you want — an area, a radius around a point,
  named stations — instead of the full fire
  hose. On a home connection the full feed is
  survivable but pointless: the map cannot
  usefully hold the planet's traffic, and
  chapter 6's filters assume you start from a
  sane slice.
- **Reconnect on failure** does what it says,
  and is what you want for a connection left
  running.

The lab made no APRS-IS connection: there was
no callsign to present that would have been
honest, and the lab's rule was to log in as
nobody. Receive-only connections without a
login are a feature of some APRS clients; in
Xastir the Internet Server properties expect
a callsign and passcode, and this guide
describes the connection as documented, not
attempted.

## Position and weather doors

- **Serial GPS** and **Networked GPS (via
  gpsd)** feed your own position from a
  receiver instead of the fixed coordinates
  of chapter 3 — the moving station's half of
  APRS. A GPS also gives Xastir accurate time.
- **Serial WX** and **Networked WX** connect
  a local weather station, whose readings
  Xastir can report and display. The shipped
  configuration includes support for the
  common station families of its era; the
  weather you *receive* from other stations
  needs no interface of your own, as the
  specimen log's weather station shows.

## The default record

A fresh install has one interface slot,
empty. From the lab's configuration file:

```text
DEVICE0_TYPE:0
DEVICE0_NAME:
DEVICE0_IGATE_OPTION:0
DEVICE0_ONSTARTUP:0
```

Type 0 is "nothing here", the igate option
(chapter 9) defaults to disabled, and nothing
starts on its own. Xastir out of the box is
a map with a station of one — which is the
honest starting point this guide's lab kept:
the traffic in chapters 6 and 8 arrives by
log file, through no interface at all, and
everything an interface would add is more of
what the specimen already shows.
