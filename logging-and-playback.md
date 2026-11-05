# Logging and Playback

Xastir can write down everything it hears,
and — the rarer trick — read it back later as
if it were happening again. The record is how
an APRS station reviews an event, debugs a
path problem, or, in this guide's case, runs
a whole lab with no radio at all: if the
traffic can be a file, the file can be the
lab.

## The logs

All five live as toggles in the **File**
menu, captured in the lab exactly as
installed:

| Log | What it records |
|---|---|
| TNC Logging | Everything to and from the TNC interfaces |
| Net Logging | Everything to and from the internet interfaces |
| IGate Logging | What the igate forwarded, and what it refused, with reasons |
| Message Logging | Message traffic |
| WX Logging | Weather data from your own weather station |

plus two snapshot switches (PNG and KML) that
save map images on an interval rather than
packet text. A fresh install has every packet
log **off** — the lab read the defaults from
the configuration file (`TNC_LOG_DATA:0`,
`NET_LOG_DATA:0`, `LOG_IGATE:0`, `LOG_WX:0`,
`LOG_MESSAGE:0`). While any log is on, the
status bar's **Logging** indicator lights —
the lab lit it once by accident during
verification and can confirm it is easy to
spot, which is the point of it.

The bundled help carries a warning this
guide repeats undiluted: **logging can fill
your hard drive.** A busy feed writes all
day; the help suggests making arrangements
to roll logs over automatically if you log
continuously. Files land in `~/.xastir/logs/`
with names by kind (`tnc.log`, `net.log`,
and kin). Xastir writes timestamp lines into
its logs every 30 seconds of operation, so a
log carries not just what was heard but when.

## What a log file is

A log line is a packet in the raw form a TNC
prints it — source, destination and path, a
colon, the payload:

```text
N0CALL-2>APRS:!4000.40N/07500.90W_090/008g014t068r000p000P000h55b10132 Fictional weather station
```

That is the entire format. No binary, no
database, nothing proprietary: a log is a
text file, readable in an editor, editable,
emailable, archivable. (The specimen log in
`examples/` was written by hand in a text
editor, in this format, which is the
strongest evidence this chapter can offer
that the format is what it claims.)

## Playback: Open Log File

**File → Open Log File** is the playback
door. The file selector opens on
`~/.xastir/logs/` — the lab verified the
default — and accepts any file of raw packet
lines. Playback feeds the file through the
same decoder the interfaces use, at reading
speed: stations appear on the map, the
station list fills, weather decodes, messages
file. Your station keeps working normally
meanwhile; playback is one more source among
the interfaces, not a mode the program
enters.

The lab's playback, as a Check block — this
is the experiment the whole guide hangs on:

Check: copy the specimen into place and play
it back —

```bash
cp examples/specimen-log.txt ~/.xastir/logs/
```

then **File → Open Log File**, select
`specimen-log.txt`, and watch three things:

1. The status bar's first segment reads
   **"File done.."** when the file is read.
2. The station counter rises from `1/1` to
   **`6/6`**.
3. View → All Stations shows the six rows of
   chapter 6, and the world map labels the
   cluster over North America, weather readout
   and all.

All three were observed in the lab, and the
screenshots are in `xastir-lab/transcripts/`.

## What playback is not

Two confusions the bundled help explicitly
guards against, both repeated here because
they are the natural mistakes:

- **Tracklogs are not logs.** The `.trk`
  files saved from a station's info window
  (chapter 6) record one station's positions
  for export to GPS and mapping tools. Open
  Log File does not read them — the help says
  so in so many words.
- **Playback is not time travel.** A log
  replays its packets, but the stations it
  creates are *new* entries stamped with the
  replay's time (the lab's list showed the
  playback date, not the packets' original
  moments, in its Pos Time column — the
  specimen's mobile position carried a
  timestamp of its own, which the map used,
  but the *hearing* was the replay's). Treat
  a replay as a fresh hearing of old words,
  and keep the original log if the timing
  itself is evidence.

## Keeping a station's memory

Used deliberately, the pair of features makes
the station self-documenting: log the event,
play it back during the debrief, keep the
file with the event's other records. An
emergency-communications exercise, a balloon
flight, a marathon — each reduces, afterwards,
to a text file anyone with Xastir can
re-hear. It is the most quietly useful thing
in the program, and it is the reason this
guide could be verified at all.
