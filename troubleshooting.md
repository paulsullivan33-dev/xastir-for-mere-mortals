# Troubleshooting

Symptom first, cause second, fix third. Every
entry here was either observed in the lab or
follows directly from a mechanism a chapter
verified; the purely documented ones say so.

| Symptom | Likely cause | Fix |
|---|---|---|
| The Configure Station dialogue opens at every start | Callsign is still `NOCALL` | Set your callsign (or accept the reminder as the price of the placeholder). Observed at every lab start while unconfigured |
| Your own station plots in the Atlantic, off West Africa | Position is the default 0°N 0°W | Set LAT/LONG in Configure Station. The ocean at those coordinates is the Gulf of Guinea; every new Xastir swims there |
| Map is empty and the counter reads `1/1` | Nothing has been heard: no interface running, nothing replayed | Start an interface (ch. 5) or play a log (ch. 8). `1/1` is you alone — the program is healthy, the world is unheard |
| Counter total grows but the view shows `1/6` | You are zoomed onto empty map | The counter is in-view / total. Find the station (Station → Find Station) or zoom out |
| Open Log File plays nothing; counter unchanged | The file is not raw packet lines — often a tracklog | Tracklogs (`.trk`) cannot be played back (bundled help is explicit). Use a TNC/Net log, or a hand-written file in the ch. 8 format |
| A hand-written message packet never files as a message | Addressee field is not exactly 9 characters | Pad the addressee with spaces to nine (`N0CALL   `); the specimen in `examples/` is a working template |
| A station shows the "wrong" comment | A newer packet replaced it | The list shows latest state by design. The packet history lives in the log, not the list |
| Weather label shows units you don't think in | Units setting differs from the packet's native imperial | Set units in File → Configure → Units of Measure; packets are always imperial, display is your choice |
| Grey map, stations floating on nothing | Online map selected but tiles never fetched | Connect once and pan your area to fill the cache (ch. 4), or select the built-in `worldhi.map` to prove plotting works |
| Shapefile map draws in one flat colour | Its `.dbfawk` styling file is missing or mismatched | Match the styling file to the data set in `/usr/share/xastir/config/`; debug with `testdbfawk` |
| The status bar says **Logging** and you didn't ask it to | A File-menu log toggle is on | Turn the five toggles off in the File menu; remember logs grow — the help's disk warning is real on a busy feed |
| Nothing from the TNC, though the cable is right | Wrong interface type, wrong port, or a TNC waiting for its startup script | Check the type list in ch. 5; the shipped `tnc-startup.*` file for your model is the usual missing piece. (Documented — the lab had no TNC) |
| Xastir ignores your `$HOME` | It is meant to | Xastir uses your account's home directory from the system account record, verified in the lab. Put the config in the real `~/.xastir/` |
| Messages arrive twice | The ack was lost, so the sender retried | Not a fault — APRS messaging is retry-until-acked by design (ch. 7) |
| Your igate forwards nothing | The igate option is off on the interface, whatever the station settings say | The per-interface option is the operative switch, and the help insists it must be set on each interface (ch. 9) |

## The three questions, in order

When a station misbehaves, the chapters
reduce to three questions worth asking before
any other debugging:

1. **What does the counter say?** `1/1` means
   nothing has been heard at all — think
   sources and interfaces. A growing total
   with an empty view means the hearing is
   fine and the *looking* is wrong — think
   zoom, filters, and map selection.
2. **What does the log say?** Turn on the
   relevant log for five minutes. Raw lines
   arriving means the pipe works and the
   problem is downstream (parsing, filtering,
   display); silence means the problem is
   upstream, in the interface, the modem, or
   the radio — in that order of likelihood
   and in reverse order of how much this
   guide can help.
3. **What does the config file say?** The
   dialogues are views onto
   `~/.xastir/config/xastir.cnf`; when a
   setting will not stay set, read the file.
   Every default quoted in this guide came
   out of that file, and every fix in this
   table ends there.
