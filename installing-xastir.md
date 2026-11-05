# Installing Xastir

## The Ubuntu package

On Ubuntu 24.04, Xastir is one package in the
universe repository, and installing it is the
whole job:

```bash
sudo apt update
sudo apt install xastir
```

The lab machine took it from the archive as
version **2.2.0-1build4**. The package pulls
in more than the program: the Motif window
libraries it is built on, GraphicsMagick for
raster maps, the curl library for internet
maps, shapelib and libgeotiff for vector and
topographic maps, libax25 for kernel AX.25
support — and the Festival speech synthesiser,
which is how a twenty-year-old APRS client
comes to install a talking robot uninvited.
It is harmless; chapter 3's siblings in the
configuration menus (audio alarms and speech)
are where it would ever be used.

Check: the version command prints the version
and exits, without needing a display —

```bash
xastir -V
```

```text
Xastir V2.2.0
```

Three helper programs arrive in the same
package, all verified present on the lab
machine:

| Program | What it is for |
|---|---|
| `callpass` | Computes an APRS-IS passcode from a callsign (chapter 5) |
| `xastir_udp_client` | Sends packets to a running Xastir over its UDP server socket |
| `testdbfawk` | Tests the shapefile styling rules of chapter 4 |

## First run

Start it from a terminal the first time, so
warnings have somewhere to be seen — the
bundled help asks for exactly this, and the
lab did it under a virtual display:

```bash
xastir &
```

On the very first run Xastir builds its
private directory tree before it draws
anything. The lab captured the whole of it:

```text
Making user dir
Making user config dir
Making user data dir
Making user log dir
Making user tracklogs dir
Making user tmp dir
Making user gps dir
Making map_cache dir
```

That tree is `~/.xastir/` in your account's
home directory, and it is worth knowing its
shape now, because later chapters keep
meeting it: `config/` holds the plain-text
configuration, `logs/` is where the chapter 8
log files live, `tracklogs/` holds saved
station tracks, and `map_cache/` is the
internet map cache of chapter 4. One
behaviour the lab verified the slightly
surprising way: Xastir finds that home
directory from your account record, not from
the `$HOME` environment variable — run it
with a different `$HOME` and it will still
build and use the real one.

It then reports which map formats this build
supports — captured verbatim in the lab and
quoted in chapter 4 — indexes the maps it
ships with, and opens the main window with
the **Configure Station** dialogue on top of
it (chapter 3). That dialogue is not a
one-time welcome screen: at every lab start
with the callsign still set to the N0CALL
placeholder, it came back. Take the hint it
is offering.

Check: after the first run, the tree and the
default configuration file exist —

```bash
ls ~/.xastir/
grep STATION_CALLSIGN ~/.xastir/config/xastir.cnf
```

```text
config  data  gps  logs  map_cache  tmp  tracklogs
STATION_CALLSIGN:NOCALL
```

## Other platforms, honestly

Only the Ubuntu package was installed for
this guide. Xastir's project also documents
building from source (the traditional route,
and the way the newest code arrives) and
packages exist in other distributions'
repositories; Windows and macOS runs go
through the usual virtualisation or
compatibility arrangements rather than a
native port. Those routes are described from
the project's documentation, not from lab
experience, and the chapters that follow
speak for the Debian/Ubuntu build: menu
wording, file locations, and the compiled-in
map support of chapter 4 are this build's,
and a source build may differ in the details.
