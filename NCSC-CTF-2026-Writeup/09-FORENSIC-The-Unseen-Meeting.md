# Proof of Concept: The Unknown Server

| Field | Detail |
|---|---|
| Challenge | The Unknown Server |
| Category | Forensics / OSINT |
| Difficulty | Hard |
| Points | 65 |
| Evidence | `evidenceimg.E01`, `IMPORTANT.png`, `Important Dates.txt` |
| Status | Solved |

## 1. Scenario

A forensic evidence archive was provided as part of the investigation, containing an EnCase forensic disk image and supporting files. The task was to recover deleted information from the imaged filesystem and use the recovered clues to determine a location and a date.

## 2. Objective

Recover the deleted meeting information from the forensic image, decode the embedded location clue, determine the associated date, and construct the challenge flag from both.

## 3. Methodology

- Extraction and inventory of the supplied evidence archive
- Analysis of an EnCase (`.E01`) forensic disk image containing an NTFS filesystem
- Recovery of a deleted file via NTFS Master File Table (MFT) examination
- A1Z26 cipher decoding of numeric references (A=1, B=2, … Z=26)
- Correlation of a secondary text clue with a known public calendar date

## 4. Investigation Steps

### Step 1 — Extract and inventory the evidence
The supplied ZIP archive contained:

```
Forensis/evidenceimg.E01
Images/IMPORTANT.png
Documents/Important Dates.txt
```

The primary artifact for analysis was the EnCase forensic image, `evidenceimg.E01`.

### Step 2 — Identify the decoding method
`Images/IMPORTANT.png` contained the clue `A1Z26`, indicating that any numeric sequences found elsewhere in the evidence should be decoded using the A1Z26 substitution cipher (A=1, B=2, … Z=26).

### Step 3 — Analyze the forensic image
The `.E01` image was mounted/examined as an NTFS filesystem. Reviewing the NTFS MFT for deleted entries recovered a deleted file, `Meeting.txt`, with the following content:

------------------------------

The location discussed earlier remains unchanged.

Reference:

10 - 1 - 14 - 20 - 1 - 18
13 - 1 - 14 - 20 - 1 - 18

The reference should be interpreted using the method recorded
in the personal notes.

(One digit in the second sequence was partially corrupted in the raw recovery but was still legibly reconstructable as `18`, consistent with the pattern of the first sequence.)

### Step 4 — Decode the location
Applying A1Z26 to each sequence:

| Sequence | Decoded |
|---|---|
| 10-1-14-20-1-18 | J-A-N-T-A-R → **JANTAR** |
| 13-1-14-20-1-18 | M-A-N-T-A-R → **MANTAR** |

Combined: **JANTAR MANTAR**.

### Step 5 — Determine the date
`Documents/Important Dates.txt` referenced "the birth anniversary of the person commonly recognized on Indian currency," specifying the year 2026. This identifies **Mahatma Gandhi**, whose birth anniversary (Gandhi Jayanti) falls on **2 October**, giving:

```
02 October 2026
```

### Step 6 — Construct the flag
Combining the decoded location and date per the challenge's required format:

```
FLAG{JANTAR_MANTAR_02-10-2026}
```

## 5. Evidence Summary

| Artifact | Value |
|---|---|
| Forensic image | evidenceimg.E01 (EnCase, NTFS) |
| Recovered deleted file | Meeting.txt (via NTFS MFT) |
| Cipher clue | A1Z26 (from IMPORTANT.png) |
| Decoded location | JANTAR MANTAR |
| Date clue source | Important Dates.txt |
| Resolved date | 02 October 2026 (Gandhi Jayanti) |

## 6. Conclusion

The visible evidence files alone did not contain the answer — the key artifact was a deleted file recoverable only through MFT-level examination of the NTFS filesystem inside the EnCase image. The `A1Z26` clue then converted two numeric sequences into a real-world landmark, and a second, independent clue file supplied the date needed to complete the flag. Both halves of the flag are corroborated by distinct pieces of recovered/supplied evidence.

## 7. Flag

```
FLAG{JANTAR_MANTAR_02-10-2026}
```
