# Proof of Concept: The Missing Connection

| Field | Detail |
|---|---|
| Challenge | The Missing Connection |
| Category | OSINT |
| Points | 30 |
| Evidence | `1787995151_cdr.csv` |
| Status | Solved |

## 1. Scenario

A mobile number suspected of association with a mule-account network was under investigation. A Call Detail Record (CDR) dump for the number was supplied, containing hundreds of call and SMS entries.

## 2. Objective

Trace the relevant communication entry in the CDR, identify the organization connected to the subject's activity, and report that organization's official website domain.

## 3. Methodology

- Structured review of the CDR CSV, separating voice records from SMS records
- Recognition of non-numeric "B Party Number" values as SMS sender IDs/headers rather than phone numbers
- TRAI SMS header registry lookup to identify the registered organization
- Verification of the organization's official website

## 4. Investigation Steps

### Step 1 — Review the CDR
The CDR contained fields including A Party Number, B Party Number, Service Type, SMS Header Type, Call Date, and Call Initiation Time. Ordinary voice/SMS entries used standard 12-digit numbers (e.g., `919801122334`, `919852019283`, `919430129384`).

### Step 2 — Isolate the SMS records
Of roughly 192 SMS records in the dump, one B Party value stood out as non-numeric:

```
TCPLIN-S
```

This appeared repeatedly across multiple dates (23–28 August 2026), unlike the standard phone-number entries.

### Step 3 — Identify the SMS header
`TCPLIN-S` is a registered SMS sender header with an appended suffix. The registered header itself is:

```
TCPLIN
```

### Step 4 — Look up the header
A TRAI (Telecom Regulatory Authority of India) SMS header lookup identified `TCPLIN` as registered to:

```
TECHFINO CAPITAL PRIVATE LIMITED
```

### Step 5 — Confirm the official domain
The organization's official website was confirmed as `https://www.techfino.in/`, giving the required domain:

```
techfino.in
```

## 5. Evidence Summary

| Field | Value |
|---|---|
| Suspicious SMS sender | TCPLIN-S |
| Registered header | TCPLIN |
| Registered organization | Techfino Capital Private Limited |
| Official domain | techfino.in |

## 6. Conclusion

The key investigative insight was recognizing that not every "B Party Number" in a CDR is a phone number — SMS sender headers can appear in the same field and serve as an independent OSINT pivot to an organization via the public TRAI header registry.

## 7. Flag

```
FLAG{techfino.in}
```
