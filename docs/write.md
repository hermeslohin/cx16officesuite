# X16 Write - word processor

`LOAD "X16WP.PRG"` and `RUN`. Needs a mouse. Files: `X16WP.PRG`; for ownCloud and the Save As
folder browser also `X16WPCL.BIN`, `X16WPSA.BIN`, `X16LINK.BIN`, `X16DOCS.BIN` (+ your `X16LINK.KEY`);
for tables `X16WPTB.BIN`; for pictures and tool tips `X16WPPI.BIN` and `X16WPPL.BIN`. Without the `.BIN`
files X16 Write is a plain SD card word processor.

## The screen

Row 0: title (file name, *modified*, page *n of m*) and the close box. Rows 1-2: icon toolbars.
Row 3: text and highlight colour swatches. Row 4: ruler. Then the page view with page borders and
a scroll bar, and the status bar (tool tips when you hover over an icon).

* **Toolbar 1**: New, Open, Save, Save As, Cut, Copy, Paste, Select All, Page Break, **Table**.
* **Toolbar 2**: Bold, Italic, Underline, Align left / center / right, Bullets, Numbers, Outdent,
  Indent, and the **font box** (click it: 3 monospace fonts - Courier New, Lucida Console, Andale
  Mono - and four sizes, **12**, **18**, **24** and **36 pt**).
* **Row 3**: 16 text colours and 16 highlight colours. On the X16 they show in the Sunset colours
  (red is a hot pink, for example); saved RTF, TXT and DOCX files use the standard colours, so a
  document looks the same in other programs as before.

## Editing

* **Click** to place the cursor, **drag** to select, **double-click** a word to select it; scroll
  bar or wheel to scroll.
* Keys: typing, Enter, Backspace, Delete, arrows, Home, End, PgUp, PgDn, Tab (4 spaces).
* Formatting buttons apply to the selection, or to what you type next.
* A page is 64 columns x 54 lines (prints as 12 pt, 10 characters per inch, 1" margins);
  up to 16 pages with the standard 512 KB of RAM, about 53 pages with 1 MB and 64 pages with 1.5 or
  2 MB (with more RAM there is also room for more pictures). Clipboard: 2700 characters.

## Tables

* **Table** button: type the size as `columns x rows`, up to **8 x 20** (for example `4x3`). The
  table goes on the current line if it is empty, otherwise after the paragraph. Columns are
  equal (with 8 columns a cell holds 6 characters, with 4 columns 14).
* Type in a cell. **Tab** = next cell (after the last cell a new row is added); **Enter** = same cell
  one row down, and out of the table from its last row. Formatting and colours work in cells.
* **Table** button with the cursor in a table: **Add row**, **Delete row**, **Delete table**.
* Tables are saved as real RTF tables, and as real Word tables in `.docx` on ownCloud; Word
  tables open as X16 Write tables (more than 8 columns are merged into the last one).

## Pictures (BMX)

* **Picture** button (toolbar 1, after Table): **1** = a BMX file from the SD card (type its name),
  **2** = from ownCloud (the `Documents` list; only `.bmx` files can be chosen). BMX is the
  Commander X16's bitmap format: version 1, uncompressed, 1, 2, 4 or 8 bits per pixel, up to 640 x 1024.
* The picture goes on the current line if it is empty, otherwise after the paragraph (or after the
  table or picture the cursor is in); there is always a line after it to go on writing.
* It is shown centred in the 16 Sunset colours and scaled to fit: a 320 x 240 picture takes 15 lines.
  A picture never starts on a page it doesn't fit on.
* The cursor can sit on a picture: **Backspace** or **Delete** removes it; **Enter**, typing or
  **Paste** go to a new line after it. Text is never merged into a picture, and a selection that
  touches a picture deletes the whole picture.
* Up to 15 pictures in about 200 KB (two full-screen 256-colour pictures, or many small ones).
* In the **RTF** file the BMX is kept exactly as it was (other programs skip it). On ownCloud the hub
  makes real pictures of them in `.docx` and `.rtf` for Word, the same size as on the X16; pictures in
  Word documents (PNG, JPEG, GIF, BMP) arrive as BMX pictures (at most 320 x 240, 256 colours, about
  160 KB per document; the rest are left out).

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
* 18 and 24 pt characters take 2 x 2 cells, 36 pt 3 x 3 cells; a line is as high as its biggest
  character (36 pt: 21 characters a line). Word documents' sizes open as the nearest of the four.
