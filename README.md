# X16 Office Suite for the Commander X16

Ready-to-run builds and user guides for a mouse-driven office suite for the
[Commander X16](https://www.commanderx16.com/): a word processor, a spreadsheet, a file manager
and a calendar. They share one look, and they all work with your own **ownCloud** server for
documents and the calendar, through a small sync hub on your network.

This repository holds **no source code**. It has the built programs (`sdcard/`), the instructions,
and links to the repositories each part is built from (see [VERSIONS.md](VERSIONS.md) for the exact
commits).

| Program | What it does | Guide | Source |
|---|---|---|---|
| **X16 Write** `X16WP.PRG` | Word processor: fonts, sizes, colours, lists, pages; RTF on the SD card, RTF/TXT/DOCX on ownCloud | [docs/write.md](docs/write.md) | [commanderx16wp](https://github.com/hermeslohin/commanderx16wp) |
| **X16 Sheets** `X16SHEETS.PRG` | Spreadsheet: formulas, functions, formats; `.xlsx` on the SD card, XLSX/CSV on ownCloud | [docs/sheets.md](docs/sheets.md) | [commanderx16sheets](https://github.com/hermeslohin/commanderx16sheets) |
| **X16 Files** `X16FM.PRG` | File manager: SD card on the left, ownCloud on the right; copy, move, rename, delete, folders | [docs/files.md](docs/files.md) | [commanderx16fm](https://github.com/hermeslohin/commanderx16fm) |
| **X16 Calendar** `CALENDAR.PRG` | Month calendar; Sync with an ownCloud (CalDAV) calendar | [docs/calendar.md](docs/calendar.md) | [commanderx16calendar](https://github.com/hermeslohin/commanderx16calendar) |
| **Sync hub** (container) | Runs on a Linux machine on your LAN; connects the X16 to ownCloud | [docs/hub.md](docs/hub.md) | [x16-office-hub](https://github.com/hermeslohin/x16-office-hub) |

```
X16 app --serial/ESP32 card (Wi-Fi)--TCP 6502--> sync hub (Docker) --HTTPS--> your ownCloud
```

## Quick start

**Just the apps (no ownCloud):**

1. Copy everything in [`sdcard/`](sdcard/) to the root of the X16's SD card (or download the
   zip from the [latest release](../../releases/latest)).
2. On the X16: `LOAD "X16WP.PRG"` and `RUN` (or `X16SHEETS.PRG`, `X16FM.PRG`, `CALENDAR.PRG`).
   You need a mouse and 512 KB of RAM.

Every app works with the SD card alone. The ownCloud parts say so politely when there is no hub.

**With ownCloud** (documents in ownCloud's `Documents` folder, the calendar in ownCloud's `X16`
calendar):

1. Run the sync hub on a Linux machine on your network: [docs/hub.md](docs/hub.md) (about 20
   minutes with Docker).
2. Fit the **TexElec X16 Serial & ESP32 Network Card** (Zimodem firmware) and put it on your Wi-Fi
   ([docs/hub.md, step 6](docs/hub.md#6-connect-the-x16)).
3. Let the hub make this X16's key file and copy **`X16LINK.KEY`** next to the apps on the SD card.

Then use **Open / Save As → 2 ownCloud** in Write and Sheets, the right-hand pane in Files, and
the **Sync** button in the Calendar.

## What goes on the SD card

All the apps live together in one folder (the SD card's root is simplest). They share the
X16Link libraries and the key file.

| File | Needed by |
|---|---|
| `X16WP.PRG`, `X16WPCL.BIN`, `X16WPSA.BIN` | X16 Write (the two `.BIN` files: ownCloud and the Save As folder browser) |
| `X16SHEETS.PRG`, `SHUI.BIN`, `SHOPS.BIN`, `SHFILE.BIN`, `SHXW.BIN`, `SHXR.BIN`, `SHSA.BIN` | X16 Sheets (all required) |
| `X16FM.PRG` | X16 Files |
| `CALENDAR.PRG` | X16 Calendar (keeps its events in `CALENDAR.DAT`, sync state in `CALSYNC.DAT`) |
| `X16LINK.BIN`, `X16DOCS.BIN` | the ownCloud link, shared by all four apps (the calendar needs only `X16LINK.BIN`) |
| `X16LINK.KEY` | **yours**, made by the hub for this X16 (never in this repository). Treat the SD card like a house key: anyone with this file can act as your X16 towards the hub. |

The files' SHA-256 checksums are in [SHA256SUMS](SHA256SUMS).

## Common to all the apps

* **Same look**, the **Sunset Arcade** theme: a striped title bar with the close box at the top
  right, a toolbar of coloured buttons (hover for a tool tip in the status bar), cream pages and
  lists on a dark violet desk, dialogs with mouse buttons and keyboard shortcuts (Enter = OK,
  Esc = Cancel). **Quill**, a little pencil at the left end of the status bar, blinks now and then
  and hops when something went well (a save, a copy, a sync).
* **Your documents keep their colours.** The theme only changes how the 16 colours look on the
  X16's screen (red shows as a hot pink, for example); RTF and XLSX files are saved with the
  original colours, so they look the same in other programs as before.
* **Save As has folders** (Write and Sheets), on the SD card and on ownCloud: double-click a
  folder to open it, `..` / **[ Up ]** to go up, **[New folder]** or **F7** to make one.
* **ownCloud never overwrites silently.** If a file changed in ownCloud since you opened it, or a
  name already exists, you choose **Overwrite**, **New name** or **Cancel**.
* **Files up to 1 MiB** travel to and from ownCloud. A dropped Wi-Fi connection resumes where it
  stopped.

## Trying it in the emulator

The official [x16emu](https://github.com/X16Community/x16-emulator) runs the apps:
`x16emu -scale 2 -fsroot sdcard -prg sdcard/X16WP.PRG -run` (`-rtc` gives the calendar today's
date). For ownCloud in the emulator, use an emulator build with the virtual Zimodem on UART1
([x16-emulator-uart](https://github.com/morphinejh/x16-emulator-uart) +
[libximodem](https://github.com/morphinejh/libximodem)) and add `-uart1 ximodem`.
For X16 Files, prefer an SD card image (`-sdcard card.img`): the emulator's host file system
(`-fsroot`) can't copy or move files between folders.

## Building from source

Each source repository builds on its own with Prog8 12.3.x, 64tass and Java 11+ (`make`, see its
README). [VERSIONS.md](VERSIONS.md) lists the commits these binaries were built from and the
toolchain.
