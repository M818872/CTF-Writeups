# Proof of Concept: The Flood's Mark

| Field | Detail |
|---|---|
| Challenge | The Flood's Mark |
| Category | OSINT (Video Geolocation) |
| Points | 20 |
| Evidence | `IMG_2728.MP4` |
| Status | Solved |

## 1. Objective

Identify the geographic location of a distinctive red-roof building shown in supplied flood footage, by comparing it against satellite/map imagery, and report its coordinates rounded to three decimal places.

## 2. Methodology

- Frame-by-frame review of the flood footage for identifiable landmarks
- Landscape and structure comparison against satellite and map imagery
- Coordinate lookup and confirmation via Google Maps

## 3. Investigation Steps

### Step 1 — Review the footage
The footage (`IMG_2728.MP4`) was reviewed to identify recognizable features — most notably the distinctive red-roof building and the surrounding terrain — that could be used to narrow the search area.

### Step 2 — Narrow the search area
The visible terrain and nearby structures in the flood footage were compared against satellite/map imagery of candidate flood-affected regions.

### Step 3 — Match the location
The building and surrounding landmarks matched an area near the **Rasuwa Customs Office**, Timure, Thuman, Bagmati Province, Nepal (Google Plus Code: `7948+8WG Thuman, Bagmati Province, Nepal`).

### Step 4 — Obtain coordinates
Placing a map pin at the matched location returned:

```
28.2558101, 85.3673248
```

Rounded to the three decimal places required by the challenge:

```
Latitude:  28.256
Longitude: 85.367
```

## 4. Evidence Summary

| Field | Value |
|---|---|
| Location | Near Rasuwa Customs Office, Timure, Thuman, Bagmati Province, Nepal |
| Raw coordinates | 28.2558101, 85.3673248 |
| Rounded coordinates (3 d.p.) | 28.256, 85.367 |

## 5. Conclusion

The location was determined by using the flood footage to constrain the search geographically before matching the specific red-roof structure — rather than searching coordinates blind. The result is independently reproducible by comparing the same footage against map imagery of the identified area.

## 6. Flag

```
FLAG{28.256,85.367}
```
