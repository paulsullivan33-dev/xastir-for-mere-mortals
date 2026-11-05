# First Run and Station Setup

## The dialogue that greets you

Xastir's first window is its main map window,
and on top of it — as captured in the lab —
sits **Configure Station**. Before you have
configured anything, Xastir wants to know who
the station is. Its fields, in order:

- **Callsign.** Pre-filled with `NOCALL`, the
  placeholder. This one field is your
  station's identity everywhere: it is what
  your beacons would claim, what your APRS-IS
  login would present, what your messages
  would carry. Put your real callsign here if
  you are licensed; if you are building a
  receive-only station, you may leave the
  placeholder — the map works either way, and
  the placeholder honestly announces that this
  station should never transmit.
- **LAT / LONG.** Your station's own position,
  entered as degrees and decimal minutes. The
  default is 00°00.000′ N, 000°00.000′ W —
  which is a real place, in the Atlantic
  Ocean south of Ghana, and is exactly where
  an unconfigured Xastir plots its own **X**
  on the world map. The lab's screenshot shows
  it there. A station in the ocean is the
  universal symptom of "position not set yet"
  (chapter 11).
- **Station Symbol.** A *group/overlay*
  character and a *symbol* character, with a
  **Select** button that opens the symbol
  table. The default pair, `/` and `x`, draws
  the plain X the lab map shows. Symbols are
  how the map reads at a glance — a house, a
  car, a weather station each have their
  character — and chapter 6 reads the
  specimen log by them.
- **Power – Height – Gain – Directivity
  (PHG).** Radio buttons for transmitter
  power, antenna height, antenna gain, and
  directionality. From them Xastir builds the
  four-digit PHG code other stations use to
  draw your approximate coverage circle. It
  only means anything for a transmitting
  station; receive-only stations can leave it
  on *Disable PHG*.
- **Comment.** Free text that rides with your
  position reports. Public by design (chapter
  1): write it for strangers.
- **Position Ambiguity.** Deliberately vague
  positions — None, or roughly 0.18 km,
  1.85 km, 18.53 km, 111.19 km of fuzz, the
  four choices the dialogue offers. Ambiguity
  exists so a station can be on the map
  without being on a doorstep; the numbers
  are the sizes of the map squares the fuzz
  corresponds to.

**OK** saves and closes; **File → Configure →
Save Config Now!** exists as a menu item
because Xastir otherwise saves configuration
at its own moments — another habit of its
age, and the bundled help gives that menu
item its own topic.

Check: the dialogue's values after OK are in
the config file in plain text —

```bash
grep -E "STATION_(CALLSIGN|LAT|LONG)" ~/.xastir/config/xastir.cnf
```

```text
STATION_CALLSIGN:NOCALL
STATION_LAT:0000.000N
STATION_LONG:00000.000W
```

## The configuration file

Everything Xastir knows about your station
lives in `~/.xastir/config/xastir.cnf`, one
`KEY:value` line at a time, editable in any
text editor while Xastir is closed. The lab
read its defaults from that file rather than
trusting the dialogues, and several later
chapters quote it: logging switches (all
`0`, off, in a fresh install), interface
definitions (chapter 5), and the igate
option (chapter 9) are all lines here. Two
rules for hand-editing: change one thing at
a time so a mistake has an obvious address,
and keep a copy of the working file before
you start — `cp xastir.cnf xastir.cnf.good`
is the whole backup strategy, and it is
sufficient.

## The main window

Behind the dialogue is the working screen,
and its furniture is worth naming once,
because the whole guide refers to it:

- **The menu bar.** File, View, Map, Station,
  Message, Interface, Help. Chapters quote
  these menus by name; the lab captured them
  as displayed, and their contents were
  plainer than most modern software dares:
  the File menu, for example, is mostly the
  logging switches of chapter 8.
- **The map.** Chapter 4's subject; at first
  run it is the built-in world map at whole-
  planet zoom, your own station's X on it.
- **The toolbar toggles.** TrackMe, Draw,
  Measure, Move, and the In/Out zoom buttons
  with pan arrows, at the top right.
- **The status bar.** The bottom strip, and
  the quickest health check in the program.
  Its segments report, left to right, the
  current activity or message; the map centre
  coordinates and Maidenhead grid square when
  the pointer has settled; the station counter
  as **in view / total known** — `1/1` at
  first run, yourself alone; the zoom level;
  and a **Logging** indicator that lights
  while any log of chapter 8 is on. The lab
  watched that counter become `6/6` during
  playback, then `1/6` after zooming to an
  empty stretch of ocean — the total is the
  program's memory, the first number is only
  what the current view contains.

Check: a healthy first run shows your own
station on the map, the counter at `1/1`, and
no dialogue left open. Everything after this
chapter is about making the counter grow.
