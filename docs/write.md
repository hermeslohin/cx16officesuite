# X16 Write - word processor

`LOAD "X16WP.PRG"` and `RUN`. Needs a mouse. Files: `X16WP.PRG`; for ownCloud and the Save As
folder browser also `X16WPCL.BIN`, `X16WPSA.BIN`, `X16LINK.BIN`, `X16DOCS.BIN` (+ your `X16LINK.KEY`).
Without the `.BIN` files X16 Write is a plain SD card word processor.

## The screen

Row 0: title (file name, *modified*, page *n of m*) and the close box. Rows 1-2: icon toolbars.
Row 3: text and highlight colour swatches. Row 4: ruler. Then the page view with page borders and
a scroll bar, and the status bar (tool tips when you hover over an icon).

* **Toolbar 1**: New, Open, Save, Save As, Cut, Copy, Paste, Select All, Page Break.
* **Toolbar 2**: Bold, Italic, Underline, Align left / center / right, Bullets, Numbers, Outdent,
  Indent, and the **font box** (click it: 3 monospace fonts - Courier New, Lucida Console, Andale
  Mono - and two sizes, **12 pt** and **24 pt**).
* **Row 3**: 16 text colours and 16 highlight colours.

## Editing

* **Click** to place the cursor, **drag** to select, **double-click** a word to select it; scroll
  bar or wheel to scroll.
* Keys: typing, Enter, Backspace, Delete, arrows, Home, End, PgUp, PgDn, Tab (4 spaces).
* Formatting buttons apply to the selection, or to what you type next.
* A page is 64 columns x 54 lines (prints as 12 pt, 10 characters per inch, 1" margins);
  up to 16 pages. Clipboard: 2700 characters.

## Files

**Open** and **Save As** first ask: **1** = SD card, **2** = ownCloud.

### SD card

* **Save As** shows a folder browser: the current folder, `..`, folders (blue, `/`) and files,
  and a name field. **Double-click a folder** (or select it with the arrow keys and press Enter)
  to open it, `..` or **[ Up ]** to go up, **[New folder]** or **F7** to make one, click a file
  to take its name. Type a name and press Enter or **[ Save ]**; Esc / [Cancel] changes nothing.
  Saving into a folder makes it the current folder, so a later Save or Open works there.
  Replacing an existing file asks first.
* Documents are **RTF**: Word, LibreOffice and ownCloud open them. X16 Write reads its own RTF
  back exactly, and other programs' RTF on a best-effort basis.

### ownCloud

* **Open** lists everything in ownCloud's `Documents` folder (with subfolders) with size, date
  and type. Arrow keys / PgUp / PgDn / wheel to move, Enter or double-click to open, Esc to cancel.
  **RTF** opens as it is; **TXT** and **DOCX** (Word) are converted by the hub. Spreadsheets and
  files over 1 MiB are greyed out.
* **Save** of a document that came from ownCloud writes it back, but only if nobody changed it in
  ownCloud meanwhile.
* **Save As** browses `Documents` (same browser as on the SD card, including New folder). The
  extension picks the format: **`.rtf`** (full formatting), **`.txt`** (plain UTF-8 text),
  **`.docx`** (a real Word document; it is saved as `.docx` again next time).
* If the name exists, or the file changed since you opened it: **Overwrite** (replaces exactly the
  version the hub showed you), **New name**, or **Cancel**.
* The status bar shows progress (`Transferring nn%`) and the result.

## Good to know

* Opening RTF from other programs: colours map by index, one font family per run.
* Large (24 pt) characters take 2 x 2 cells; a line with large text is two rows high.
