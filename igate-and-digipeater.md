# The Igate and Digipeater Question

Every feature before this chapter can run
with the transmitter silent. This one
cannot. An **igate** (internet gateway)
copies traffic between the radio and APRS-IS
in both directions; a **digipeater** repeats
radio packets so they travel further. Both
make your station part of the network's
plumbing — other people's packets move
because your station decided to move them —
and both are transmitting, with a licensed
operator responsible for every repetition.

The verification line is short and total: the
lab configured nothing in this chapter, gated
nothing, and repeated nothing. The defaults
and menu placements below were read from the
lab's configuration file and Xastir's bundled
help; the behaviour is documented-only, and
the chapter's real content is the duties,
which do not need a lab.

## What Xastir offers

**Igate options are per-interface.** In each
interface's properties (chapter 5) an igate
setting chooses the device's gateway role;
the bundled help is explicit that you must
choose an igate option *on each interface*
for the gateway to function, and the default
is off. The lab's default record carries it:

```text
DEVICE0_IGATE_OPTION:0
```

Station-level settings (File → Configure)
hold the other half: whether the station is
an igate at all, and — for weather — whether
National Weather Service alert traffic may be
forwarded to RF, which Xastir additionally
gates on a station list file
(`nws-stations.txt`): weather warnings are
not forwarded on a whim or by default.

**Digipeating in Xastir is the RELAY kind.**
The TNC interface properties offer a *RELAY
Digipeat* switch: Xastir repeats a packet
when the first unused alias in its path is
your callsign or one of up to 50 callsigns
listed on the config file's `RELAY_DIGIPEAT_CALLS`
line. The bundled help frames the intended
use precisely, and this guide quotes its
sense plainly: relay digipeating is for
filling gaps in regions where there are few
other fill-in digipeaters. It is a shovel,
not a lifestyle.

## The duties

1. **A licence and your own callsign.**
   Every repeated packet goes out under your
   station's responsibility. The passcode
   rules of chapter 5 apply with double
   force: an igate speaks to APRS-IS *as
   you*.
2. **RF → internet is the easy direction,
   and still a decision.** Gating what you
   hear to APRS-IS makes your receiver part
   of the world's picture. That is usually a
   service — it is how most stations on
   aprs.fi got there — but it publishes other
   people's traffic under your gateway's
   name, and the igate log (chapter 8) exists
   so you can answer for what you forwarded.
3. **Internet → RF is the direction that
   needs a reason.** Everything you gate onto
   the air consumes a shared, narrow channel
   that local stations are trying to beacon
   into. Gate narrowly — messages addressed
   to local stations are the classic
   legitimate load — and never gate the
   general feed. The network's etiquette
   here is not decorative; a bad igate can
   silence a county.
4. **Digipeat only a real gap.** A digipeater
   duplicates every packet it repeats, at
   full channel cost. Where a WIDE digipeater
   already covers the area, a home relay adds
   collisions, not coverage. The help's
   framing (few other fill-ins) is the test:
   if the gap is not demonstrable, leave the
   switch off.
5. **Log it, and read the log.** Enable igate
   logging before the gateway, not after the
   first surprise. Xastir records forwards
   and refusals with reasons; that record is
   the difference between running a gateway
   and merely having started one.

Check: on a correctly idle station — one that
listens only — the configuration file shows
the igate option at `0` on every interface
and no RELAY digipeat enabled. If you find
either on and cannot say when you turned it
on or why, this chapter is your reminder to
turn it back off until you can.
