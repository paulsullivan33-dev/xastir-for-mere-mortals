# Reading the Map

This chapter is the lab's evidence read
closely. Everything in it comes from the
nine-line specimen log of chapter 1, played
back as chapter 8 describes, and the views
below were captured from that playback. The
raw packets are in `examples/specimen-log.txt`;
nothing here asks to be taken on trust.

## The station list: the memory behind the map

**View → All Stations** after playback listed
six entries. Cleaned of the window's
truncation, they were:

| # | Symbol | Call Sign | Packets | Path | PHG | Comment |
|---|---|---|---|---|---|---|
| 1 | house | N0CALL | 2 | APRS | | Fictional home station |
| 2 | digipeater | N0CALL-1 | 1 | APRS,WIDE2-2 | PHG5130 | Fictional digipeater |
| 3 | weather | N0CALL-2 | 1 | APRS | | Fictional weather station |
| 4 | car | N0CALL-9 | 4 | APRS | | Moving east on a fictional road |
| 5 | X | N0CALL | 0 | local | | |
| 6 | object | PICNIC | 1 | APRS | | Fictional picnic object |

Read the columns, because they are the
client's whole model of a station:

- **Packets** counts what was heard from that
  station. N0CALL-9's four are its two
  positions, its message, and its status —
  the count is of packets, not positions.
- **Path** is the route the last packet took.
  The digipeater's own beacon travelled as
  `APRS,WIDE2-2`: addressed to APRS, asking
  digipeaters for two more hops.
- **Comment** is always the *latest* one.
  N0CALL-9's first position said "Fictional
  mobile station"; its second said "Moving
  east on a fictional road", and the list
  shows the second. The list is a table of
  current state, not an archive — the archive
  is the log file (chapter 8).
- Rows 1 and 5 are the same callsign twice,
  and both are correct. Row 5, path `local`,
  0 packets, is *your* station — the one
  chapter 3 configured. Row 1 is a station
  *heard* using the same callsign (the
  specimen uses N0CALL for its home station
  too, because N0CALL is nobody). Xastir
  keeps "me" and "heard" apart, and a real
  station list will show your own callsign
  the same way whenever your beacons come
  back to you through a digipeater or the
  internet.

## Symbols: the map's shorthand

Each row's icon is drawn from the packet's
symbol table and code — `/` table, `>` code
for the car; `-` for the house; `#` for the
digipeater; `_` for weather; the object's
code for PICNIC. The symbol set is APRS-wide,
not Xastir's invention: the same codes mean
the same pictures in every client, which is
why a map from any program reads like a map
from any other. Two practical notes. A
station's symbol is chosen by the *sending*
station and can lie — a car symbol on a
stationary station is a configuration
mistake there, not a decoding mistake here.
And overlays (a letter or digit in place of
the `/`) refine a symbol's meaning; Xastir
draws the base symbol with the overlay
character on it.

## Tracks: a station that moves

N0CALL-9 reported twice, about half a
kilometre apart, course roughly east. Xastir
joins a mobile station's positions into a
**track**: the line is the station's recent
history drawn on the map, and the station's
current symbol sits at its head. A track is
only ever as dense as the station's beacon
rate — two points make a straight line and a
suggestion, not a route — and it ages out
with the station. **Station → Track Station**
follows a chosen station as it moves, and the
station info window (right-click a station)
can store a track to disk as `.trk`, KML, and
shapefile copies under `~/.xastir/tracklogs/` —
exports, note, not recordings: chapter 8 is
clear that track files cannot be played back.

## Weather: decoded, converted, displayed

On the world map after playback, the weather
station's label carried a second line, the
lab's favourite capture in this guide:

```text
T:20°C  H:55%  S:14km/h  G:21km/h  C:90°
```

That is N0CALL-2's packet —
`_090/008g014t068…h55b10132` — fully decoded:
wind from 090° at 8 mph gusting 14, 68°F,
55% humidity, pressure 1013.2 hPa. Xastir
displayed it in metric (20°C, 14 and 21 km/h)
because the lab's units were set that way;
the packet itself is imperial, as APRS
weather format always is. The point of the
exercise is the division of labour: the
packet carries numbers in fixed positions,
the client owes you units you think in.
**View → Weather Stations** lists every
weather source with its readings in tabular
form, and a station's own weather (chapter
5's WX interfaces) appears under Own Weather
Data.

## Finding, filtering, asking

Three tools keep a busy map legible, all
verified as present in the lab's menus:

- **Station → Find Station** centres a named
  station at the current zoom — the fastest
  answer to "where is that callsign I just
  heard?" Its dialogue was captured in the
  lab, callsign typed and all.
- **View** splits the station list by kind —
  Mobile Stations, Local Stations, Last
  Stations, Weather Stations, Objects &
  Items — and **Station → Filter Data /
  Filter Display** narrow what the map draws
  by age, distance, and station type. On a
  full internet feed, filtering is not
  cosmetic: it is the difference between a
  map of your county and modern art.
- **Right-clicking a station** opens its info
  box: full position, course and speed,
  altitude where reported, the path history,
  and the actions — send a message, store the
  track, run the queries of chapter 7. The
  bundled help's station-info topic is the
  full inventory.

Check: play the specimen back and open View →
All Stations. Six rows, the car's comment
reading "Moving east on a fictional road",
and the weather station carrying PHG's empty
chair beside the digipeater's PHG5130 — if
your table matches this chapter's, your
decoder, your symbols, and this guide all
agree.
