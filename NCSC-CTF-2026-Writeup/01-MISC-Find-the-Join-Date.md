# Proof of Concept: Find the Join Date

| Field | Detail |
|---|---|
| Challenge | Find the Join Date |
| Category | OSINT |
| Points | 5 |
| Target | Instagram account `@ncs.council` |
| Status | Solved |

## 1. Objective

The challenge required identifying the date on which the Instagram account `@ncs.council` was originally created, using only publicly accessible account information (no external evidence files were supplied).

## 2. Methodology

Instagram exposes limited account-creation metadata to any viewer through its built-in **"About this account"** panel, accessible from a profile's options menu. This feature was used directly, without any third-party tooling.

## 3. Investigation Steps

1. **Target identification** — The account `@ncs.council` was opened and confirmed as the account referenced in the challenge.
2. **Metadata access** — From the profile, the **About this account** panel was opened.
3. **Data extraction** — The panel displayed the following account metadata:

   | Field | Value |
   |---|---|
   | Date joined | August 2026 |
   | Account based in | India |
   | Verified | August 2026 |


## 4. Finding

The account `@ncs.council` was created on Instagram in **August 2026**.

## 5. Conclusion

This was a single-step OSINT lookup using a built-in, publicly available Instagram feature — no scraping, automation, or exploitation was involved. The finding is directly reproducible by any investigator viewing the same panel.

## 6. Flag

```
FLAG{Augest_2026}
```
