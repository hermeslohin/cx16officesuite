# Versions

The files in `sdcard/` were built on 2026-11-25 from fresh clones of these commits (six themes shared by all four apps, picked by clicking Quill; X16 Write
with tables, 12/18/24/36 pt, BMX pictures and up to 64 pages with more RAM, and the hub that converts them to and from DOCX; X16 Write and
X16 Sheets without the flashing title bar, toolbars and status bar; X16 Write scrolls through every page of long documents; X16 Write shows pictures in 256 colours and inserts PNG, JPEG, GIF and BMP files from ownCloud; X16 Write keeps long documents in swap files on the SD card, up to 8192 lines on every X16; every app's X returns to a visible READY prompt on real hardware, the ownCloud link forces RTS/CTS flow control on the ESP32 card, and X16Link reads the serial card from main RAM, so real X16s receive $FF bytes intact):

| Component | Repository | Commit | Files |
|---|---|---|---|
| X16 Write | [hermeslohin/commanderx16wp](https://github.com/hermeslohin/commanderx16wp) | [`06614eb`](https://github.com/hermeslohin/commanderx16wp/commit/06614eb0e47c66906089636732fa229e41a2ea2a) | X16WP.PRG, X16WPCL.BIN, X16WPSA.BIN, X16WPTB.BIN, X16WPPI.BIN, X16WPPL.BIN, X16WPHC.BIN, X16WPTH.BIN, X16WPVM.BIN, X16THEME1-6.BIN |
| X16 Sheets | [hermeslohin/commanderx16sheets](https://github.com/hermeslohin/commanderx16sheets) | [`e981ace`](https://github.com/hermeslohin/commanderx16sheets/commit/e981aceb37af0becb8e2b32c0b9812efb94e70a9) | X16SHEETS.PRG, SHUI/SHOPS/SHFILE/SHXW/SHXR/SHSA/SHTH.BIN |
| X16 Files | [hermeslohin/commanderx16fm](https://github.com/hermeslohin/commanderx16fm) | [`eea8a80`](https://github.com/hermeslohin/commanderx16fm/commit/eea8a80228d7cbd8c8fa8e6d3dcc1caf7241a063) | X16FM.PRG |
| X16 Calendar | [hermeslohin/commanderx16calendar](https://github.com/hermeslohin/commanderx16calendar) | [`1cca8c4`](https://github.com/hermeslohin/commanderx16calendar/commit/1cca8c42c38f2225f54d45f441158843a7a32b80) | CALENDAR.PRG |
| Sync hub + X16Link library | [hermeslohin/x16-office-hub](https://github.com/hermeslohin/x16-office-hub) | [`2b7a970`](https://github.com/hermeslohin/x16-office-hub/commit/2b7a9700b5e7cc04b51e8d3abb6bb5d13b642d27) | X16LINK.BIN, X16DOCS.BIN; image ghcr.io/hermeslohin/x16-office-hub:sha-2b7a970 (X16Link reads the UART through a stub in golden RAM $06FC-$06FF; the hub answers a resent HELLO or AUTH again) |

`X16LINK.BIN` and `X16DOCS.BIN` come out byte-identical from every app's vendored copy of the X16Link library; one copy serves all the apps. The same goes for `X16THEME1.BIN` ... `X16THEME6.BIN` (made by `tools/mkthemes.py`, identical in every app repository). Checksums: [SHA256SUMS](SHA256SUMS).

## Toolchain

* Prog8 v12.3.5 (`prog8c`), 64tass Turbo Assembler Macro V1.60.3243, Java 21.0.1
* Built for the Commander X16 ROM R49 and later; tested in x16emu R49/R50 (with the virtual Zimodem for the ownCloud parts) on FAT32 SD card images.

## Rebuilding

Clone a repository at the commit above and run `make` (Calendar: `make sd SD=<dir>`, with the folder made first; Write: `./build-cloud.sh <dir>`; Sheets and Files: `./build.sh <dir>`). Each copies its files under the names used here.
