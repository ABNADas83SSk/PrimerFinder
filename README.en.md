# Primer Finder

[日本語](README.md) · English

Created by Akira Yoshinari with ChatGPT. Primer Finder searches a local Excel primer list against a DNA sequence in your browser.

## Getting started

1. Select **Code → Download ZIP** on GitHub and extract the archive.
2. Open `PrimerFinder_en.html` in Chrome or Edge. Use `PrimerFinder.html` for Japanese.
3. Click **Select Excel file** and select your local primer workbook.
4. Paste a DNA sequence or a single FASTA record.
5. Choose **Exact match** or **Allow mismatches**, enter the maximum mismatch count if needed, and click **Search**.

No installation or local server is required. Use an unencrypted `.xlsx` file no larger than 30 MB.

## Workbook format

The app reads the first worksheet.

| Column | Content |
| --- | --- |
| A | Primer ID |
| B | Optional notes (not searched) |
| C | Primer sequence, 5′→3′ |

Whitespace is removed and sequences are converted to uppercase. Empty sequence rows are ignored. Rows containing characters outside ACGTRYSWKMBDHVN are skipped.

## Matching and results

- Full-length primers are searched in both forward and reverse-complement orientations.
- Allow mismatches accepts up to the specified number of substitutions. Insertions and deletions are not included.
- Ambiguous bases such as N and R are compared literally rather than expanded as wildcards.
- Positions are 1-based and inclusive, relative to the input sequence.
- Repeated and overlapping matches are included. Palindromic primers are reported once per position as ±.
- Sequence context follows the input orientation. Mismatched bases are colored and underlined.
- The total match count is shown, with the first 5,000 matches listed. Large mismatch searches may take time.

## Dropbox updates

1. Put the HTML file and `primers.xlsx` in the same shared Dropbox folder.
2. Make that folder available offline on each computer.
3. Open the HTML file from Finder or File Explorer. Click **Connect shared folder** and select the folder each time you open the app.
4. Save workbook updates under the same filename. After Dropbox syncs the changes locally, the app checks for updates approximately every five seconds while open. Existing results are recalculated using the same search settings.

Folder access depends on browser support and permission. When unavailable, use **Select Excel file** again after each update. Updates depend on Dropbox completing its own sync.

## Data handling

Workbook parsing and sequence matching run locally in the browser. The HTML app does not send primer lists or query sequences, load external libraries, or use analytics. Files stored in Dropbox remain subject to Dropbox sharing and synchronization.

Primer lists are excluded from this repository. The included `.gitignore` excludes Excel workbooks and common sequence file formats.

## Validation

The original app was checked in Chromium for Excel parsing, exact and mismatch searches, both orientations, mismatch highlighting, and simulated folder updates. Actual Dropbox synchronization needs to be checked in the user's environment.
