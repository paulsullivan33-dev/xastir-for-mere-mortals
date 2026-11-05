# Writing Criteria

Every guide in this repo is written to the same
standard. If you're adding or editing a guide —
human or AI — hold it to these.

1. **Plain words, real ideas.** Simple language,
   never dumbed-down concepts. Explain jargon on
   first use; collect terms in the glossary.
2. **No hype.** No marketing adjectives, no
   "revolutionary," no promises about what
   something will do for the reader.
3. **Honest about limits.** Say what the thing
   *can't* do. State uncertainty instead of
   smoothing it over. Validation notes include
   what remains unverified.
4. **No invented numbers.** Benchmarks, defaults,
   and specs are either measured or qualified with
   "depends on your setup." If it wasn't tested,
   say so.
5. **Checkable.** Commands are meant to be run,
   with "Check:" blocks showing what success looks
   like. Sources are linked, not asserted.
6. **Respect the reader's setup.** Call out
   Windows/Mac/Linux differences. Don't assume a
   GPU, a budget, or prior experience.
7. **Safety isn't skipped.** Real risks get
   stated plainly, not buried.
8. **Scoped.** Each guide says what it covers and
   points elsewhere for the rest. No guide
   pretends to be the whole subject.
9. **Structure over prose.** Tables, before/after
   examples, symptom → fix. Scannable beats essay.

## Verification notes for this guide

Standard 3 and 4 applied to this guide,
specifically. **The build machine had no
radio.** Ubuntu 24.04, no TNC, no GPS, no
receiver of any kind, and no APRS-IS login —
the lab's rule was to log in as nobody, and
Xastir's Internet Server properties expect a
callsign and passcode, so no internet
connection was attempted. What the lab had
was the program itself (Ubuntu package
xastir 2.2.0-1build4), a virtual X display
(Xvfb), its bundled help file, its default
configuration file, and one nine-line
specimen log. The guide is built from what
those honestly produce: the first-run
behaviour, the real configuration defaults,
the menus as displayed, and a complete
playback decode. Working transcripts and
screenshots are kept with the build
(`xastir-lab/transcripts/`).

**The lab.** Two halves. (1) *The specimen:*
`examples/specimen-log.txt`, nine lines of
raw TNC-format APRS text written by hand for
this guide — a digipeater position with
PHG5130, a home position, two mobile
positions forming a track, one weather
report, one object (PICNIC), one message and
its ack, one status text. Every station is
the N0CALL placeholder family; every position
is a round number near 40.00°N 75.00°W;
nothing in it is a real station, a real
place's occupant, or a received signal.
(2) *The playback:* the specimen was copied
into `~/.xastir/logs/` (the directory the
Open Log File selector opens by default,
verified) and opened through File → Open Log
File under a scripted X session. The status
segment read "File done..", the station
counter rose from 1/1 to 6/6, and View →
All Stations listed all six entries — the
four specimen callsigns, the PICNIC object,
and the local station — with symbols, packet
counts (the mobile's 4 = 2 positions +
message + status), paths, the digipeater's
PHG5130, and latest comments matching the raw
lines. The weather packet displayed as
"T:20°C H:55% S:14km/h G:21km/h C:90°" —
68°F and 8/14 mph converted by the program's
metric units setting, arithmetic checked
against the packet's `t068`, `090/008g014`,
and `h55` fields.

**Verified by running, per chapter:**

- *Ch. 2:* the package install from the
  Ubuntu archive; `xastir -V` printing
  "Xastir V2.2.0" with no display; the
  helpers `callpass`, `xastir_udp_client`,
  and `testdbfawk` present in /usr/bin; the
  linked libraries via `ldd` (Motif,
  GraphicsMagick, libcurl, shapelib,
  libgeotiff, libproj, libax25).
- *Ch. 2–3:* the first-run console output
  (the "Making user …" directory lines,
  captured whole); the Configure Station
  dialogue as displayed (callsign NOCALL,
  00/000 defaults, symbol `/x`, the PHG radio
  groups, the four position-ambiguity
  choices), reappearing at a later start
  while the callsign remained NOCALL; the
  own-station X plotted at 0,0 on the world
  map; the default configuration values
  quoted (`STATION_CALLSIGN:NOCALL`,
  `STATION_LAT:0000.000N`,
  `STATION_LONG:00000.000W`, all logging
  switches 0, `DEVICE0_TYPE:0`,
  `DEVICE0_IGATE_OPTION:0`) read from
  `~/.xastir/config/xastir.cnf`; the
  `$HOME`-independence of the config
  location, found accidentally (a run with a
  different `$HOME` still used the account's
  real home) and then relied on.
- *Ch. 4:* the startup banner's map-type
  list, quoted verbatim; `selected_maps.sys`
  defaulting to `worldhi.map`; the shipped
  Online map definitions (five `.geo` files)
  and the Mapnik file's OSM tiled-map lines,
  read from `/usr/share/xastir/maps/Online/`.
- *Ch. 5:* the interface type list, quoted
  from the bundled help's "Configuring
  Interfaces" topic; the shipped
  `tnc-startup.*`/`tnc-stop.*` files in
  `/usr/share/xastir/config/`; `callpass
  N0CALL` printing "Passcode for N0CALL is
  13023" (the placeholder callsign's code,
  published here because it is nobody's
  credential — the algorithm is public and
  the callsign is a placeholder; your own
  callsign's code should be treated as a
  password and is never printed in this
  guide).
- *Ch. 6–8:* the playback and its evidence
  as described in The lab, above; the File,
  View, Station, and Message menus captured
  as displayed (File's five logging toggles
  and two snapshot toggles; View's station
  list family; Station's Find/Track/Filter
  items; Message's nine items); the Find
  Station dialogue, including typing the
  specimen callsign into it; the status
  counter's in-view/total behaviour (6/6 at
  world zoom, 1/6 zoomed onto empty ocean);
  the status bar's Logging indicator, lit
  once by an accidentally toggled log during
  verification and then deliberately read.
- *Ch. 8:* the Open Log File selector's
  default directory (`~/.xastir/logs/`),
  observed directly.

**Capture hygiene (declared trims):** the
All Stations table in chapter 6 is the
captured window with its columns widened in
prose — the window truncated comments at its
edge ("Fictional digipeater – s…"); the full
comments are the specimen file's own words.
Screenshots were taken on a virtual display
shared early in the session with other
programs' windows; the captures kept here
are from a private display and show only
Xastir. Sandbox timestamps in screenshots
are the build machine's clock (November
2026 in its reckoning) and are weather, not
claims.

**Documented-only (not run), and why:**

- *Every live interface:* serial and KISS
  TNCs, kernel AX.25, GPS receivers, weather
  station hardware. No such device existed.
  Types, properties, and the AGWPE door are
  described from the bundled help; the Dire
  Wolf pairing is described from the sibling
  guide's verified account of its own side.
- *APRS-IS connections in either direction:*
  no login was made. Xastir's Internet
  Server properties expect a callsign and
  passcode; the lab had no callsign it could
  honestly present, and receive-only access
  without one is not how this client's
  interface is shaped. Filters, reconnect
  behaviour, and passcode handling are from
  the bundled help.
- *All transmitting:* beacons, message
  composition and sending, queries, objects
  of one's own, bulletins. Sending is
  licensed amateur activity; the lab is
  receive-side by construction, and the
  sending desk is described from the
  captured menus and the bundled help.
- *Igate and digipeater operation:* nothing
  was gated or repeated. Defaults were read
  from the configuration file; behaviour and
  the per-interface rule are from the
  bundled help's Serial TNC and Configure
  Station topics.
- *Online tile rendering:* tiles were never
  fetched. The `.geo` definitions and the
  cache arrangement are described from the
  shipped files; every screenshot shows the
  built-in world map.
- *Installation beyond apt:* source builds
  and other distributions are named from
  the project's documentation; only the
  Ubuntu package was installed.
- *The neighbours:* YAAC, APRSIS32,
  PinPoint, APRSdroid, Soundmodem, and
  aprs.fi were not installed or used; each
  is characterised from its project's own
  description, in one paragraph, unranked.

Specimen discipline, for the record: the
specimen log is synthetic in the open. Its
stations use the placeholder callsign APRS
software itself ships with, its object is an
avowedly fictional picnic, and its positions
are round numbers. No real station was
heard, recorded, impersonated, or logged
into at any point in this build; the sandbox
received no RF and made no network
connection to any APRS server.
