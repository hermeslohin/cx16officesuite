# Versions

The files in `sdcard/` were built on 2026-11-18 from fresh clones of these commits (Sunset Arcade look; X16 Write
with tables, and the hub that converts them to and from DOCX):

| Component | Repository | Commit | Files |
|---|---|---|---|
| X16 Write | [hermeslohin/commanderx16wp](https://github.com/hermeslohin/commanderx16wp) | [`afb5ae2`](https://github.com/hermeslohin/commanderx16wp/commit/afb5ae26360aa5160a4c879192193adb1aa8e2a7) | X16WP.PRG, X16WPCL.BIN, X16WPSA.BIN, X16WPTB.BIN |
| X16 Sheets | [hermeslohin/commanderx16sheets](https://github.com/hermeslohin/commanderx16sheets) | [`d3f3b2c`](https://github.com/hermeslohin/commanderx16sheets/commit/d3f3b2cbcca26e9dde893bb2de9b44af07aabbe6) | X16SHEETS.PRG, SHUI/SHOPS/SHFILE/SHXW/SHXR/SHSA.BIN |
| X16 Files | [hermeslohin/commanderx16fm](https://github.com/hermeslohin/commanderx16fm) | [`100560c`](https://github.com/hermeslohin/commanderx16fm/commit/100560ca009379e667786dd28853e77ec005d2e9) | X16FM.PRG |
| X16 Calendar | [hermeslohin/commanderx16calendar](https://github.com/hermeslohin/commanderx16calendar) | [`2de10de`](https://github.com/hermeslohin/commanderx16calendar/commit/2de10de11ded0fb53a8a2e21b37981a7b090f6e8) | CALENDAR.PRG |
| Sync hub + X16Link library | [hermeslohin/x16-office-hub](https://github.com/hermeslohin/x16-office-hub) | [`45833be`](https://github.com/hermeslohin/x16-office-hub/commit/45833be4ebf31fa77a31935277b7dee9f9230239) | X16LINK.BIN, X16DOCS.BIN; image ghcr.io/hermeslohin/x16-office-hub:sha-45833be (tables in DOCX) |

`X16LINK.BIN` and `X16DOCS.BIN` come out byte-identical from every app's vendored copy of the X16Link library; one copy serves all the apps. Checksums: [SHA256SUMS](SHA256SUMS).

## Toolchain

* Prog8 v12.3.5 (`prog8c`), 64tass Turbo Assembler Macro V1.60.3243, Java 21.0.1
* Built for the Commander X16 ROM R49 and later; tested in x16emu R49/R50 (with the virtual Zimodem for the ownCloud parts) on FAT32 SD card images.

## Rebuilding

Clone a repository at the commit above and run `make` (Calendar: `make sd SD=<dir>`, with the folder made first; Write: `./build-cloud.sh <dir>`; Sheets and Files: `./build.sh <dir>`). Each copies its files under the names used here.
