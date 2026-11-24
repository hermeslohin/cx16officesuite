# Versions

The files in `sdcard/` were built on 2026-11-24 from fresh clones of these commits (six themes shared by all four apps, picked by clicking Quill; X16 Write
with tables, 12/18/24/36 pt, BMX pictures and up to 64 pages with more RAM, and the hub that converts them to and from DOCX; X16 Write and
X16 Sheets without the flashing title bar, toolbars and status bar; X16 Write scrolls through every page of long documents; X16 Write shows pictures in 256 colours and inserts PNG, JPEG, GIF and BMP files from ownCloud; X16 Write keeps long documents in swap files on the SD card, up to 8192 lines on every X16; every app's X returns to a visible READY prompt on real hardware, and the ownCloud link forces RTS/CTS flow control on the ESP32 card):

| Component | Repository | Commit | Files |
|---|---|---|---|
| X16 Write | [hermeslohin/commanderx16wp](https://github.com/hermeslohin/commanderx16wp) | [`fa2928b`](https://github.com/hermeslohin/commanderx16wp/commit/fa2928b1843887faf5889ffd87ad741f2cdc9b7c) | X16WP.PRG, X16WPCL.BIN, X16WPSA.BIN, X16WPTB.BIN, X16WPPI.BIN, X16WPPL.BIN, X16WPHC.BIN, X16WPTH.BIN, X16WPVM.BIN, X16THEME1-6.BIN |
| X16 Sheets | [hermeslohin/commanderx16sheets](https://github.com/hermeslohin/commanderx16sheets) | [`619e906`](https://github.com/hermeslohin/commanderx16sheets/commit/619e906919bc818df2520180e5b2b3c680d03fc5) | X16SHEETS.PRG, SHUI/SHOPS/SHFILE/SHXW/SHXR/SHSA/SHTH.BIN |
| X16 Files | [hermeslohin/commanderx16fm](https://github.com/hermeslohin/commanderx16fm) | [`801efed`](https://github.com/hermeslohin/commanderx16fm/commit/801efede17418b70a951f6ba431c5d3f9403d41a) | X16FM.PRG |
| X16 Calendar | [hermeslohin/commanderx16calendar](https://github.com/hermeslohin/commanderx16calendar) | [`0a27cbf`](https://github.com/hermeslohin/commanderx16calendar/commit/0a27cbf4f6e4378416c8c575167fee5a71ee6733) | CALENDAR.PRG |
| Sync hub + X16Link library | [hermeslohin/x16-office-hub](https://github.com/hermeslohin/x16-office-hub) | [`ecc110d`](https://github.com/hermeslohin/x16-office-hub/commit/ecc110d79e768ab193a296ce3c5e931ecb5aeba6) | X16LINK.BIN, X16DOCS.BIN; image ghcr.io/hermeslohin/x16-office-hub:sha-ecc110d (a resent AUTH is answered again instead of "already authenticated"; X16Link forces RTS/CTS with ATE0F0) |

`X16LINK.BIN` and `X16DOCS.BIN` come out byte-identical from every app's vendored copy of the X16Link library; one copy serves all the apps. The same goes for `X16THEME1.BIN` ... `X16THEME6.BIN` (made by `tools/mkthemes.py`, identical in every app repository). Checksums: [SHA256SUMS](SHA256SUMS).

## Toolchain

* Prog8 v12.3.5 (`prog8c`), 64tass Turbo Assembler Macro V1.60.3243, Java 21.0.1
* Built for the Commander X16 ROM R49 and later; tested in x16emu R49/R50 (with the virtual Zimodem for the ownCloud parts) on FAT32 SD card images.

## Rebuilding

Clone a repository at the commit above and run `make` (Calendar: `make sd SD=<dir>`, with the folder made first; Write: `./build-cloud.sh <dir>`; Sheets and Files: `./build.sh <dir>`). Each copies its files under the names used here.
