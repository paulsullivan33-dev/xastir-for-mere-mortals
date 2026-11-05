# Maps

A map under the stations is not decoration:
the whole point of APRS position reports is
that they land somewhere recognisable. Xastir
keeps maps as files, layers the ones you
select, and caches what the internet sends
it. This chapter covers what the Ubuntu
build ships, what it can read, and how the
offline story works.

## The built-in world map

A fresh install has exactly one map selected:
`worldhi.map`, a simple vector world that
ships with the program. It is the map in
every lab screenshot — continents as outlines,
no roads, no labels worth the name. Its job
is to prove the program works and to give
ocean-spanning zooms something to draw; the
lab's playback used it at whole-world zoom,
where the specimen stations appeared over
North America with their labels legible. For
a neighbourhood, it has nothing to say, and
that is what the other map types are for.

Check: the default selection is a file, like
everything else here —

```bash
cat ~/.xastir/config/selected_maps.sys
```

```text
worldhi.map
```

## What this build can read

At first run Xastir prints its map support to
the terminal. Captured from the lab, verbatim:

```text
Built-in map types:
      gnis   USGS GNIS Datapoints
       pop   USGS GNIS Datapoints w/population
       map   APRSdos Maps
       map   WinAPRS/MacAPRS/X-APRS Maps

Support for these additional map types has been compiled in:
       geo   Image Map (ImageMagick/GraphicsMagick library, many formats allowed)
       geo   URL (Internet maps via libcurl library)
       geo   URL (OpenStreetMaps via libcurl library
                  Copyright OpenStreetMap and contributors, CC-BY-SA)
       shp   ESRI Shapefile Maps (Shapelib library)
       tif   USGS DRG Geotiff Topographic Maps (libgeotiff/libproj)
```

In plain words, four families matter to a
new station:

| Family | What it is | Where it comes from |
|---|---|---|
| Online tiles (`.geo`) | OpenStreetMap-style tile servers, fetched as you pan | The internet, cached locally |
| Shapefiles (`.shp`) | Vector maps: roads, boundaries, weather zones | GIS data sets, styled by `.dbfawk` rule files |
| GeoTIFF (`.tif`) | Scanned topographic maps pinned to coordinates | USGS DRG archives |
| Raster images (`.geo`) | Any image with a calibration file beside it | Scans, screenshots, satellite views |

The **Map Chooser** (Map menu) is where maps
are selected and layered; selected maps draw
in chooser order under the stations. The
package ships a large set of `.dbfawk`
styling files in `/usr/share/xastir/config/`
— the rules that decide what colour a
shapefile's roads and water draw in — which
you only need to know about when a shapefile
map renders in one flat colour: the styling
file for its data set is missing or
mismatched, and `testdbfawk` exists to debug
exactly that.

## Online maps and the cache

The package ships ready-made online map
definitions in `/usr/share/xastir/maps/Online/`:

```text
OSM_tiled_mapnik.geo
OSM_tiled_cycle.geo
OSM_tiled_fosm.geo
USTigermap.geo
USTigermapBorders.geo
```

A `.geo` file for a tiled map is short enough
to read whole. The load-bearing lines of the
Mapnik one, from the shipped file: it selects
the tiled-OSM machinery (`OSM_TILED_MAP-mapnik`)
and names the tile server
(`URL http://tile.openstreetmap.org/`). Tiles
are fetched as the map pans and zooms, and
they accumulate in the map cache —
`~/.xastir/map_cache/` in the directory tree
of chapter 2 (the `.geo` file's comments also
describe an `OSMtiles` cache directory used
by the static-map variant). Two honest
consequences:

- **First view of an area needs the
  internet.** No connection, no tiles, grey
  background — the stations still plot, on
  nothing. The lab, which did not connect
  Xastir to any map server, shows the built-in
  world map in every screenshot for this
  reason; online tile rendering is therefore
  documented-only in this guide, described
  from the shipped files rather than captured.
- **Second view does not.** Cached tiles are
  the offline story: pan over your area once
  while connected, at the zooms you will use,
  and the cache serves it later without a
  connection. That is the standard APRS field
  practice — cache the county before the
  event, not during it.

Respect the tile servers: they are donated
infrastructure with usage policies. Xastir's
pattern — interactive viewing with a local
cache — is the use they exist for; bulk
downloading regions tile by tile is not, and
the cache-by-panning habit above stays on
the right side of that line by construction.

## Finding places, and bookmarks

Two navigation aids from the bundled help,
both under the Map and Station menus' orbit:

- **Map Display Bookmarks** store a map
  position and zoom under a name, so "the
  repeater site" or "the finish line" is one
  activation away instead of a pan-and-zoom
  expedition.
- **Locate Map Feature** jumps to a named
  place when the USGS GNIS data files are
  installed; the `gnis` map types in the
  startup banner are that same data appearing
  as map points.

**Station → Find Station** is the third way
to move the map, and the one the lab used: it
centres a heard station at the current zoom.
Its dialogue — a callsign field, Match Case
and Match Exact switches, Locate Now — was
captured in the lab, and chapter 6 shows the
station list it complements.

Check: with the specimen log played back
(chapter 8), the map shows six stations over
the built-in world map, and View → All
Stations lists every one. If your map is
empty at that point, the fault is in the
playback, not the map — chapter 11 separates
the two.
