# X16 Calendar

`LOAD "CALENDAR.PRG"` and `RUN`. Needs a mouse. Events are saved to `CALENDAR.DAT` (next to the
program) after every change. For Sync with ownCloud also `X16LINK.BIN` and your `X16LINK.KEY`.
Set the X16's clock so **Today** knows the date (the hub also sets it at every Sync).

## The screen

Title bar with the close box - toolbar - entry bar (selected date, Cancel, OK, the event text) -
month grid (each day shows its first two events; `+n more`) - the selected day's events - status
bar with tool tips.

**Toolbar**: New, Edit, Delete, Cut, Copy, Paste, Today, previous / next year, previous / next
month, **Sync** (cloud) and **Conflicts** (warning sign; highlighted when there are any). The right
side shows the month and how many of the 128 event slots are used.

## Using it

* **Click** a day to select it; click an event to select it.
* **Double-click** a day (or an empty row of the day list) to add an event; **double-click** an
  event to edit it. Or just start typing: that starts a new event on the selected day.
  Return saves, Esc cancels.
* Start the text with a time, like `14:30 Dentist`, for a timed event; anything else is all-day.
  The day list is sorted, so timed events come first.
* **Drag** an event onto another day to move it. Cut / Copy / Paste copy an event to the selected day.
* **Wheel** over the month = previous / next month.
* Keys: arrows move between days, PgUp/PgDn month, Home today, Tab next event, Del delete,
  **F1** Sync, **F3** Conflicts, Ctrl+X quit.
* Limits: 6 events per day, 128 in all, 27 characters per event.

## Sync with ownCloud

Click **Sync** (or F1). The calendar saves `CALENDAR.DAT`, connects to the hub and:

* sends new, changed and deleted events to your ownCloud calendar (`X16`, the hub creates it),
* brings back what changed in ownCloud (from your phone, the web interface, ...),
* saves the result, and remembers the sync point in `CALSYNC.DAT`.

The status bar says what happened, for example `Synced. Sent: +2 changed 1 deleted 0  received 3`.
If anything goes wrong, nothing is lost: the calendar reloads what it saved and the next Sync
simply repeats.

**Conflicts**: if the same event was changed on the X16 and in ownCloud since the last Sync, the
X16 version is kept and the event gets a red `!`. The **Conflicts** button lists each one (what
changed, what ownCloud had, which version was kept); **Acknowledge all** clears the marks at the
next Sync.

Good to know: ownCloud events that don't fit (a day with more than 6, or all 128 slots used) stay
in ownCloud and the status bar says how many. Recurring ownCloud events come over one occurrence
at a time, within the hub's sync window around today.
