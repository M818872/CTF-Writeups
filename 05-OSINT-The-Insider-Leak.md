# Proof of Concept: The Insider Leak

| Field | Detail |
|---|---|
| Challenge | The Insider Leak |
| Category | OSINT |
| Points | 25 |
| Evidence | `url.txt` |
| Status | Solved |

## 1. Scenario

The Cyber Crime Unit received a complaint regarding unauthorized disclosure of internal organizational information. Sensitive records were found compiled in a publicly accessible online spreadsheet, apparently published by someone with internal access.

## 2. Objective

Identify the Google Account ID of the account used to publish the leaked spreadsheet.

## 3. Methodology

- Extraction of the Google Sheets Document ID from the supplied URL
- Use of `xeuledoc` (an open-source OSINT tool that queries Google's own document-metadata endpoints) to recover account information tied to a Google Document ID

## 4. Investigation Steps

### Step 1 — Inspect the evidence
`url.txt` contained a direct link to a publicly accessible Google Spreadsheet titled **"CONTACTS"**.

### Step 2 — Extract the Document ID
Google Sheets URLs follow the pattern `https://docs.google.com/spreadsheets/d/<DOCUMENT_ID>/...`. The extracted Document ID was:

```
1qA2PPO_LjScgN43yj5U4Z-YfsyMtop45GCGkAtF5A9Y
```

### Step 3 — Query document metadata
The Document ID was passed to `xeuledoc`:

```bash
xeuledoc 1qA2PPO_LjScgN43yj5U4Z-YfsyMtop45GCGkAtF5A9Y
```

### Step 4 — Obtain the Google Account ID
The tool returned the Google Account ID associated with the document's creation:

```
02777014063221940756
```

## 5. Evidence Summary

| Field | Value |
|---|---|
| Document type | Public Google Spreadsheet ("CONTACTS") |
| Document ID | 1qA2PPO_LjScgN43yj5U4Z-YfsyMtop45GCGkAtF5A9Y |
| Tool used | xeuledoc |
| Recovered Google Account ID | 02777014063221940756 |

## 6. Conclusion

Even a "public" Google document exposes metadata about its originating account through Google's API responses, independent of the document's visible content. This ID can be used as a pivot point for further attribution (e.g., correlating against known employee Google accounts) in the broader investigation.

## 7. Flag

```
FLAG{02777014063221940756}
```
