# Proof of Concept: The Lost Bag

| Field | Detail |
|---|---|
| Challenge | The Lost Bag |
| Category | OSINT |
| Points | 15 |
| Status | Solved |

## 1. Scenario

A bag recovered during routine police proceedings contained no ID, phone, or other item directly identifying its owner. The only lead was a torn, partially damaged academic result document showing a programme name, examination period, roll number, registration number, and an institutional logo.

## 2. Objective

Identify the institution that issued the document and, from its publicly available result records, determine the full name of the student the fragment belonged to.

## 3. Methodology

- Visual identification of the institutional logo
- Targeted web search for the identified institution
- Review of the institution's official, publicly published examination result notifications
- Cross-referencing the fragment's visible details (programme, roll/registration number format, examination period) against the matching result sheet

## 4. Investigation Steps

### Step 1 — Examine the recovered fragment
The visible fragment contained an institutional logo alongside partial academic details: programme, roll number, registration number, and result information. The logo was the strongest lead, since it was intact enough to identify the source institution.

### Step 2 — Identify the institution
The logo was matched to **Baba Ghulam Shah Badshah University (BGSBU)**, located in Rajouri, Jammu & Kashmir.

### Step 3 — Locate the relevant result notification
BGSBU publishes examination results publicly on its website. The document fragment corresponded to a **BBA Semester-VI** result, which narrowed the search to:

| Field | Value |
|---|---|
| Result Notification No. | 52 of 2026 |
| Date | 10-07-2026 |
| Examination | BBA Semester-VI, held May 2026 |

### Step 4 - Match the registration number

I compared the registration number from the recovered fragment with the registration numbers in the official result sheet.

The fragment showed:

U/23/267-BBA

The matching entry in the result sheet was:

Field

Value

Registration Number

BGSBU/23/267-BBA

Roll Number

11-BBA-2023

Name of Candidate

Yassir Mushtaq

The registration number matched the same student record, confirming the candidate as Yassir Mushtaq.

## 5. Evidence Summary

```
BABA GHULAM SHAH BADSHAH UNIVERSITY
Rajouri (J&K) - 185234

Result Notification No. 52 of 2026
Date: 10-07-2026
Result of BBA Semester-VI, Examination held May 2026

Matched Candidate: Yassir Mushtaq
```

## 6. Conclusion

Working from the institutional logo alone, this investigation reached a positively identified individual through a documented, publicly verifiable trail: logo → institution → official result publication → candidate record. Every step is independently reproducible by checking the same public university record.

## 7. Flag

```
FLAG{YASSIR_MUSHTAQ}
```
