# Proof of Concept: Operation Ghost Developer

| Field | Detail |
|---|---|
| Challenge | Operation Ghost Developer |
| Category | OSINT |
| Difficulty | Easy |
| Points | 25 |
| Target | https://kashmirnaturalbox.com/ |
| Status | Solved |

## 1. Scenario

A public website (`kashmirnaturalbox.com`) is currently active, but the organization that originally developed and managed it is no longer associated with the site.

## 2. Objective

Identify the historical developer company from archived website information, then identify the larger parent company behind that developer, and report the parent company's official website domain.

## 3. Methodology

- Wayback Machine review of historical site snapshots (since the current live site no longer shows the original developer credit)
- Website footer analysis on the archived capture
- Social-media (Instagram) correlation to trace the developer's organizational affiliation

## 4. Investigation Steps

### Step 1 — Check historical site versions
Because the challenge explicitly stated the original developer was no longer associated with the live site, the **Wayback Machine** was used instead of the current site. The archived portfolio page was retrieved:

```
https://kashmirnaturalbox.com/elements/pages/portfolio/
```

### Step 2 — Read the footer credit
The archived page's footer displayed:

```
Developed by Webium Technologies
```

This identified the developer company: **Webium Technologies**.

### Step 3 — Investigate the developer's social presence
Webium Technologies' Instagram account was located and reviewed. The account contained an identifying reference that appeared to connect it to a separate organization referred to as **CSIB**.

### Step 4 — Trace the parent-company relationship
The CSIB-linked account was the lead toward the parent company the challenge asked for.

## 5. Evidence Summary

| Field | Value |
|---|---|
| Live site | kashmirnaturalbox.com |
| Historical developer (via Wayback footer) | Webium Technologies |
| Related organization lead | CSIB |
| Parent company |
| Parent company domain |

## 6. Conclusion

** The investigation began with the historical version of the Kashmir Natural Box website using the Wayback Machine. The archived portfolio page revealed the developer as Webium Technologies.

Further OSINT investigation of Webium Technologies led to its Instagram presence, where an associated ID provided the link to the CSIB account. Following this connection established that CSIB was the parent company behind the developer organization..

## 7. Flag

```
FLAG{csib.co.in}
```
