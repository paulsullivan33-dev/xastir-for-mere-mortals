# Messaging and Bulletins

Positions are the famous half of APRS;
messages are the useful half. APRS messaging
is text with delivery machinery: a message is
addressed to one station, carries a short
line of text, and — when it asks for one —
expects an acknowledgement, with the sender
retrying until the ack arrives or patience
runs out. Everything runs over the same
broadcast medium as the beacons: a message is
a packet anyone can hear, addressed so that
mostly one station cares.

The verification line: the specimen log
contains a message and its ack, and chapter
6's list shows both were received and filed
by the lab's Xastir (the message is one of
N0CALL-9's four counted packets). Composing
and sending were not exercised — sending is
transmitting, and chapter 1's rule applies —
so the sending desk is described from the
menus the lab captured and Xastir's bundled
help.

## The specimen's message

Two of the nine lines:

```text
N0CALL-9>APRS::N0CALL   :Fictional message from the specimen log{01
N0CALL>APRS::N0CALL-9 :ack01
```

Anatomy: the `:` data type opens a message;
the addressee is padded to nine characters
(`N0CALL   `); the text follows; and `{01`
is the message identifier — the handle the
acknowledgement quotes. The second line is
the whole ack protocol in one packet: a
message back, whose entire text is `ack01`.
The sending station retries its message until
that packet (or the patience limit) arrives.
On a map full of stations this is why a
message can arrive twice: an ack was lost,
not the message, and the retry is a duplicate
by design rather than an error.

## The message desk

The **Message** menu, captured verbatim in
the lab, is the desk's whole furniture:

| Menu item | What it does |
|---|---|
| Send Message To | Compose to a chosen station |
| Show Pending Messages | Your outbox: what awaits an ack |
| Open Group Messages | Messages to groups you belong to |
| Clear All Outgoing Messages | Abandon the retries |
| General Stations Query | Broadcast a `?APRS?`-style query |
| IGate Stations Query | Ask local igates to identify (`?IGATE?`) |
| WX Stations Query | Ask weather stations for reports |
| Modify / Enable Auto Reply Message | Answer while you're away from the desk |
| Satellite Ack Mode | Acks suited to satellite passes |

**View → Message Traffic** is the filing
cabinet: every message seen, to anyone, in
order — the receive-side window the lab's
specimen message would appear in. Messages
addressed to your station raise the incoming
side of the desk; messages to others simply
pass through the log, visible because APRS
has no private channels (chapter 1's
strangers rule, again).

Group messages deserve their sentence: a
message can be addressed to a *group* name
instead of a callsign — a club, a net, an
event — and every station configured to
listen for that name files it under Open
Group Messages. It is the closest thing APRS
has to a mailing list, and it works by
nothing more than shared agreement on the
name.

## Bulletins and announcements

A **bulletin** is a message addressed to
everyone: `BLN` addresses with a number, sent
by stations with something area-wide to say —
a road closure, a repeater outage, an event
announcement, a weather warning's human
layer. **View → Bulletins** collects them.
Announcements are bulletins with a longer
lease of life, repeated on a schedule by the
sending station until cancelled. Reading
bulletins costs nothing and needs no licence;
issuing one is transmitting, with the
ordinary duties, plus one bulletin-specific
duty: cancel it when it stops being true. A
stale bulletin is worse than none, because
the system's whole design assumes bulletins
are current.

## Queries: asking the room

The three Query items in the menu are
messages that ask questions of whoever can
answer: general queries, igate queries, and
weather queries. Responses come back as
ordinary packets and land in the ordinary
places — the map, the weather list, the
station info box. A query is also
transmitting, and on a shared frequency it is
good manners to query narrowly (the station,
the area) rather than ask the whole room
questions it mostly cannot answer.

Check: after playing back the specimen,
N0CALL-9 shows four packets in View → All
Stations — and you can account for every one:
two positions, this chapter's message, and
chapter 1's status line. If your count is
three, the message line failed to parse; the
commonest cause in hand-written packets is
the addressee field — it must be exactly
nine characters, spaces included, or the
message is not a message.
