# X16 Files - file manager

`LOAD "X16FM.PRG"` and `RUN`. Needs a mouse. Files: `X16FM.PRG`; for the ownCloud pane also
`X16LINK.BIN`, `X16DOCS.BIN` and your `X16LINK.KEY`. Without them the SD card side still works and
the ownCloud pane says why it is unavailable.

**Left pane: the X16's SD card. Right pane: ownCloud `Documents`.** Copy and move files and whole
folders between the two or inside one of them; rename, delete, make folders.

## The screen

Title bar with the close box - toolbar - two panes (title, folder path, column header, list with
a scroll bar, item count) - status bar. The **active pane** has a blue title; the toolbar's arrows
point from it to the other pane. Rows: `..` (to go up), then folders (blue, `/`), then files, each
sorted by name. The status bar shows the selected file's size (and date, on ownCloud). Grey files
can't be transferred (name not representable, or over 1 MiB).

## Mouse

| Do | Result |
|---|---|
| click | select a row (and make its pane active) |
| double-click a folder / `..` | open it / go up |
| **right click** | mark / unmark a row: operations then work on all marked rows |
| **drag** rows to the other pane | **copy** them there (dropped on a folder row: into that folder) |
| **drag** rows onto a folder (or `..`) in the same pane | **move** them into it |
| wheel, scroll bar | scroll |

## Toolbar and keys

| Button | Key | |
|---|---|---|
| **Copy >** / **< Copy** | F5 | copy the marked rows (or the selected one) into the other pane's folder |
| **Move >** / **< Move** | F6 | the same, then delete the originals (only those that copied completely) |
| **Duplicate** | F3 | copy inside the same side, to a new name or path (asks) |
| **Rename** | F2 | rename, or move to another folder: type a name, or a full path like `/LETTERS/2026/mom.rtf` |
| **Delete** | F8, Del | delete (asks first); folders are deleted **with everything in them** |
| **New folder** | F7 | make a folder in the active pane's folder |
| **Refresh** | F1 | read both sides again (and retry the hub if it was unreachable) |
| | Tab | switch panes |
| | arrows, PgUp/PgDn, Home/End | move the selection |
| | Enter / Backspace | open the folder / go up |
| | Space, `*` | mark and move down / mark everything (or clear the marks) |
| **[X]** | Esc | quit (Esc asks first) |

## How copying works

* **Nothing is replaced silently**: if a file or folder of that name is already there you choose
  **Overwrite**, **All** (overwrite the rest of this operation), **Skip** or **Cancel**.
  **Esc** stops a running operation between two files.
* **Folders** are copied as whole trees in both directions (merged into a folder of the same name
  if there is one). Paths are limited to 63 characters on both sides.
* Transfers are **byte for byte**: any file type, including programs (`.PRG`) and data (`.BIN`).
  Text files are not converted (a `.txt` arrives exactly as it was). Files up to 1 MiB.
* A download first goes to `X16FM.TMP` in the destination folder; it replaces the target only
  after its checksum is right, so a failed download never damages an existing file. A dropped
  connection resumes by itself.
* SD card sizes are shown in KB and are approximate (the X16's DOS counts 254-byte blocks).

## Good to know

* X16 Files keeps the hub key in memory while it runs (it reconnects when the hub drops an idle
  session after 5 minutes) and wipes it when you quit.
* In the emulator, use an SD card image (`-sdcard card.img`): the emulator's host file system
  (`-fsroot`) can't copy or move files between folders. Real hardware is fine.
