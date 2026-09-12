# Proof of Concept: The Seized Conversation

| Field | Detail |
|---|---|
| Challenge | The Seized Conversation |
| Category | OSINT |
| Points | 45 |
| Status | Solved |

## 1. Scenario

During a digital investigation, officers seized a mobile device belonging to a suspect. A recovered screenshot showed a conversation referencing an incident, but neither the location nor the organization involved was named directly. A numerical reference embedded in the conversation was the only lead provided.

## 2. Objective

Determine which police station the two individuals in the conversation were referring to.

## 3. Methodology

- Treating the numerical reference as a case/FIR-style identifier rather than an arbitrary number
- Searching India's public **e-Courts** case information system for a matching case record
- Cross-verifying the result against independently published Delhi Police station listings and court records

## 4. Investigation Steps

### Step 1 — Examine the recovered evidence
The screenshot contained a numerical reference consistent with a legal/case record identifier. Rather than attempting to interpret the conversation's context alone, this number was used directly as an OSINT search pivot.

### Step 2 — Search public case records
Searching the reference against the **e-Courts** public case information system returned a matching case under **State of NCT of Delhi**.

### Step 3 — Extract case details
The matching case record listed:

| Field | Value |
|---|---|
| State | State of NCT of Delhi |
| Police Station | Baba Haridas Nagar |

### Step 4 — Cross-verify
"Baba Haridas Nagar" was confirmed as an official, currently operating Delhi Police station, and the same station name appears in publicly available Delhi High Court case records referencing "P.S. Baba Haridas Nagar" — providing independent confirmation from a second public source.

## 5. Evidence Summary

| Field | Value |
|---|---|
| Source | e-Courts case record, State of NCT of Delhi |
| Identified station | Baba Haridas Nagar |
| Cross-verification | Delhi Police station listing; Delhi High Court case records |

## 6. Conclusion

The unexplained numerical reference in the seized conversation functioned as a direct pivot into India's public court-records system. Two independent public sources — the e-Courts case record and separately published court/police records — agree on the same police station, giving confidence in the finding.

## 7. Flag

```
FLAG{BABA_HARIDAS_NAGAR}
```
