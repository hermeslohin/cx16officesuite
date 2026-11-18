# Versions

The files in `sdcard/` were built on 2026-11-18 from fresh clones of these commits:

| Component | Repository | Commit | Files |
|---|---|---|---|
| X16 Write | [hermeslohin/commanderx16wp](https://github.com/hermeslohin/commanderx16wp) | [`e277303`](https://github.com/hermeslohin/commanderx16wp/commit/e27730357701404d3725ce35ced1dda3b15ee3f4) | X16WP.PRG, X16WPCL.BIN, X16WPSA.BIN |
| X16 Sheets | [hermeslohin/commanderx16sheets](https://github.com/hermeslohin/commanderx16sheets) | [`810002c`](https://github.com/hermeslohin/commanderx16sheets/commit/810002c8880fa71eed33e44bb535d6c4010eda0c) | X16SHEETS.PRG, SHUI/SHOPS/SHFILE/SHXW/SHXR/SHSA.BIN |
| X16 Files | [hermeslohin/commanderx16fm](https://github.com/hermeslohin/commanderx16fm) | [`a1284ae`](https://github.com/hermeslohin/commanderx16fm/commit/a1284aea84d075af5d06b3fcecab60e2a8cb892b) | X16FM.PRG |
| X16 Calendar | [hermeslohin/commanderx16calendar](https://github.com/hermeslohin/commanderx16calendar) | [`3f728ad`](https://github.com/hermeslohin/commanderx16calendar/commit/3f728add217731cd8fc0cdb56bce3ab835a2099c) | CALENDAR.PRG |
| Sync hub + X16Link library | [hermeslohin/x16-office-hub](https://github.com/hermeslohin/x16-office-hub) | [`b4760d2`](https://github.com/hermeslohin/x16-office-hub/commit/b4760d22614848c8fd34473cf4438e6f78a23b9f) | X16LINK.BIN, X16DOCS.BIN; image ghcr.io/hermeslohin/x16-office-hub:sha-b4760d2 |

`X16LINK.BIN` and `X16DOCS.BIN` come out byte-identical from every app's vendored copy of the X16Link library; one copy serves all the apps. Checksums: [SHA256SUMS](SHA256SUMS).

## Toolchain

* Prog8 v12.3.5 (`prog8c`), 64tass Turbo Assembler Macro V1.60.3243, Java 21.0.1
* Built for the Commander X16 ROM R49 and later; tested in x16emu R49/R50 (with the virtual Zimodem for the ownCloud parts) on FAT32 SD card images.

## Rebuilding

Clone a repository at the commit above and run `make` (Calendar: `make sd SD=<dir>`; Write: `./build-cloud.sh <dir>`; Sheets and Files: `./build.sh <dir>`). Each copies its files under the names used here.
