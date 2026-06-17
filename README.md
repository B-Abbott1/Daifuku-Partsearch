# Part Number Lookup — User Guide

Look up **internal company part numbers** (Full SKU) from a list of manufacturer. Everything runs in your web browser—no login, no install, and your files never leave your computer.

---

**Recommended browsers:** Microsoft Edge, Google Chrome, or Firefox (current version).

---

## What you need

| Item | Description |
|------|-------------|
| **Product Master file** | An Excel workbook (`.xlsx`), such as a **Product Master Report** export. |
| **Part numbers to look up** | A list copied from Excel or another source—one part number per line. |

You upload a fresh master file each time you open the app (or when you need newer data). The master file is **not** stored on GitHub; each person uploads their own copy for that session.

---

## How to use it (step by step)

### Step 1: Upload the master file

1. Open the app.
2. Under **Step 1: Upload Master File**, click **Choose Excel file**.
3. Select your Product Master `.xlsx` file.
4. Wait for the loading message to finish. Large files (tens of thousands of rows) can take a little while—this is normal.
5. When loading succeeds, you’ll see a green message with how many rows were loaded (for example, *Loaded 67,272 rows*).

If loading fails, check that the file is `.xlsx`, not corrupted, and that it’s the standard Product Master layout (see [Master file format](#master-file-format) below).

### Step 2: Paste part numbers and search

1. Under **Step 2: Paste Part Numbers**, paste your list into the box—**one part number per line**.
2. Click **Search**.
3. Review the summary (for example, *42 of 50 matched*).

**Matching rules:**

- Not case-sensitive (`tl504kq` matches `TL504KQ`).
- Extra spaces at the start or end of a line are ignored.
- The tool searches **Full SKU**, **manufacturer part number**, **sc manufacturer part number**, **Daifuku Japan part number**, and **sMaterialDescription** (exact phrase within the cell text).
- Your pasted order is preserved (including blank lines and duplicate part numbers).
- **sMaterialDescription** matches only when your text appears exactly in the cell—not as part of a longer word or number (e.g. `Light 1234` does not match `Light 12345`).

### Step 3: Copy results back into Excel

After a search, a **Copy internal part numbers** box appears above the detailed table.

- Each line is the internal **Full SKU** for that row of your pasted list.
- Lines that did not match show **`not found`**.
- Click **Copy to clipboard**, or click inside the box, press **Ctrl+A**, then **Ctrl+C**.
- In Excel, click the cell where you want the first result and press **Ctrl+V**—one value per row, aligned with your original list.

This is the fastest way to fill a column in an existing spreadsheet without using the full download.

### Step 4 (optional): Download full results

Click **Download Results** to save an Excel file (`.xlsx`) with:

- The part number you searched
- Match status (Matched / Not Found)
- Which column matched (Manufacturer vs Daifuku Japan)
- Extra product fields (description, cost, inventory, and others configured for your site)

Use this when you need more than just the internal part number column.

---

## Understanding the results

### Copy box (quick paste into Excel)

| What you see | Meaning |
|--------------|---------|
| A numeric SKU (e.g. `2029014`) | Match found—internal Full SKU |
| `not found` | No matching row in the master file for that line |
| Blank line | Your pasted list had an empty line on that row |

### Results table

| Column | Meaning |
|--------|---------|
| **Searched Part Number** | What you pasted |
| **Match Status** | Matched or Not Found |
| **Matched Via** | Which column matched (`FullSKU`, `ManufacturerPartNumber`, `scManufacturerPartNumber`, `scDaifukuJapanPartNumber`, or `sMaterialDescription`) |
| **FullSKU** (and other columns) | Product details from the master file |

---

## Master file format

The app reads the **first worksheet** in the workbook.

Typical Product Master exports look like this:

- **Row 1:** Report title (e.g. *Product Master Report, Generated on …*) — ignored for matching
- **Row 2:** Column headers
- **Row 3+:** Product data

Important column names (must match the export exactly):

| Column name | Used for |
|-------------|----------|
| `FullSKU` | Internal company part number (shown in copy box and results) |
| `ManufacturerPartNumber` | Search: manufacturer / vendor part numbers |
| `scManufacturerPartNumber` | Search: sc manufacturer part numbers |
| `scDaifukuJapanPartNumber` | Search: Daifuku Japan part numbers |
| `sMaterialDescription` | Search: exact phrase within material description text (e.g. `Light 1234` will not match `Light 12345`) |

Other columns (product name, description, cost, price, etc.) may appear in the full download depending on how the site was configured.

### Keeping master data up to date

1. Export or save the latest Product Master Report as `.xlsx`.
2. Open the app and upload the new file under Step 1.

You do **not** need to wait for a GitHub update when only the Excel data changes—just upload the new export.

---

## Tips and best practices

- **One part number per line** when pasting from Excel: copy a single column, not a whole table at once (unless you only need the first column).
- **Same row count:** The copy box returns one line per line in your paste, so you can paste results beside your original list in Excel.
- **Duplicates:** If you paste the same part number twice, you’ll get two result lines (same behavior as two separate rows).
- **Large master files:** First load may take several seconds; leave the tab open until the success message appears.
- **New browser tab:** Upload the master file again—data is cleared when you close or refresh the page.

---

## Privacy and security

- All processing happens **in your browser**.
- The master file and your pasted list are **not uploaded to a server**.
- Nothing is saved after you close the tab (unless you download or copy results yourself).

Use the same care you would with any internal product data: only use trusted devices and networks.

---

## Troubleshooting
| Problem | What to try |
|---------|-------------|
| Upload never finishes | Use a smaller test file first; close other heavy tabs; try Edge or Chrome. |
| “Column not found” error | Confirm the file is a standard Product Master export with expected header names. |
| Everything shows `not found` | Check you pasted manufacturer or Daifuku Japan numbers, not internal Full SKUs (unless those columns are enabled for search). |
| Copy button doesn’t work | Click in the copy box, **Ctrl+A**, **Ctrl+C** manually. |
| Results look stale | Re-export the master from your source system and upload again. |
| Site won’t open | Confirm the GitHub Pages URL with your admin; try a hard refresh (**Ctrl+F5**). |
