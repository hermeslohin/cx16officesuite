# X16 Sheets - spreadsheet

`LOAD "X16SHEETS.PRG"` and `RUN`. Needs a mouse. Files (all required): `X16SHEETS.PRG`, `SHUI.BIN`,
`SHOPS.BIN`, `SHFILE.BIN`, `SHXW.BIN`, `SHXR.BIN`, `SHSA.BIN` (+ `SHTH.BIN` and `X16THEME1.BIN` ... `X16THEME6.BIN` for themes: click Quill for the next one); for ownCloud also `X16LINK.BIN`,
`X16DOCS.BIN` (+ your `X16LINK.KEY`).

## The screen

Row 0 title / close box - rows 1-2 icon toolbars - row 3 formula bar - column letters - 23 rows of
grid - horizontal scroll bar - status bar (tool tips; **Sum** and **Count** of the selection).

* **Toolbar 1**: New, Open, Save, Save As | Cut, Copy, Paste, Select All | Clear | Bold |
  Align left, Center, Align right.
* **Toolbar 2**: AutoSum, Insert function | Number format General, 0.00, Percent, Currency |
  Insert rows, Delete rows, Insert columns, Delete columns | Narrower, Wider.
* **Formula bar**: cell name, Cancel (X), Enter (tick), Insert function (fx), contents.

## Using it

* **Click** a cell to select it, **drag** to select a range; click a column letter / row number for
  whole columns / rows, the corner for everything. Wheel or scroll bars to scroll.
* **Type** to replace a cell, **double-click** (or F2, or click the formula bar) to edit it.
  Return = enter and move down, Tab = enter and move right, Esc = cancel, arrows move.
  Delete / Backspace clear the cells (formats stay); the Clear icon removes formats too.
* Numbers: `12`, `-3.5`, `1e6`, `$1,234.50` (sets Currency), `12%` (0.12, sets Percent).
  A leading `'` makes anything text.
* **Formulas** start with `=`. While typing one, **click or drag over cells** to insert `B2` or
  `B2:D9`. Missing `)` are added for you.
  * Operators `+ - * / ^ %`, comparisons `= <> < > <= >=` (1 or 0), parentheses.
  * Functions: `SUM AVERAGE MIN MAX COUNT PRODUCT ABS SQRT INT ROUND IF` (the fx menu lists them).
  * References `A1`, `$A$1`, `A$1`, ranges `A1:C9`. Errors: `#DIV/0! #VALUE! #REF! #NAME? #NUM!`.
* **AutoSum** on a range puts a SUM under each column (or right of a row); on a cell it proposes the
  numbers above (or to the left): Return accepts, or drag another range.
* **Copy / Paste** adjust relative references (`$` keeps them). Copy one cell, select a range,
  Paste = fill. Cut + Paste moves without changing references.
* **Insert / delete rows and columns**: formulas follow; references into deleted cells become `#REF!`.
* **Column width**: drag the right edge of a column letter, or Narrower / Wider.

## Files

**Open** and **Save As** first ask: **1** = SD card, **2** = ownCloud (only when the X16Link files
are on the SD card).

* Sheets are **`.xlsx`** files that Excel, LibreOffice and ownCloud open as they are.
* **SD card Open** shows the `.xlsx` files of the current folder. `.xlsx` files made by other
  programs are compressed: open those **through ownCloud** (the hub converts them).
* **Save As** (SD card and ownCloud) is a **folder browser**: double-click a folder (or arrows +
  Enter) to open it, `..` / **[ Up ]** to go up, **[New folder]** or **F7** to make one, click a
  file to take its name, type a name, Enter. On the SD card the chosen folder becomes the current
  one (Save and the SD Open picker then work there); replacing a file asks first.
* **ownCloud Open** lists `Documents`; `.xlsx` and `.csv` can be opened (the hub converts any xlsx
  or csv). **Save** writes back only if nobody changed the file meanwhile. **Save As** `.xlsx`
  (stored as a normal compressed xlsx) or `.csv` (values, UTF-8). Conflicts ask **Overwrite /
  New name / Cancel**.

## Limits

* Columns A-IV (256), rows 1-9999; texts up to 50 characters, formulas up to 46.
* **6400 cells** on a 512 KB X16, up to 12288 with 2 MB.
* One worksheet per file; no charts, merged cells, dates (they arrive as numbers or text), text
  functions or cross-sheet references. No undo.
