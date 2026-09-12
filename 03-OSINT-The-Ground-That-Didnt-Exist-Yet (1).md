# Proof of Concept: The Ground That Didn't Exist Yet

| Field | Detail |
|---|---|
| Challenge | The Ground That Didn't Exist Yet |
| Category | OSINT (Satellite Imagery) |
| Points | 20 |
| Status | Solved |

## 1. Scenario

Historical satellite imagery from 2022 showed an unfinished rectangular clearing in the hills of northern India. Later imagery of the same location showed a completed synthetic football ground. The challenge stated the site was associated with a university located in a Union Territory of northern India.

## 2. Objective

Use satellite imagery comparison to locate the football ground and identify the associated educational institution.

## 3. Methodology

- Comparative analysis of historical vs. current satellite imagery (Google Earth / Google Maps)
- Geographic narrowing based on the "university in a Union Territory, northern India" constraint
- Coordinate verification against map labels and institutional infrastructure

## 4. Investigation Steps

### Step 1 — Narrow the search area
The constraints given — northern India, a university situated in a Union Territory, hilly terrain, and a rectangular clearing later converted into a football ground — were used to focus the imagery search on universities in the region matching this terrain profile.

### Step 2 — Locate the football ground
A matching rectangular synthetic football ground was located at approximately:

```
33.3960° N, 74.3448° E
(more precisely: 33°23'45.6"N 74°20'41.3"E)
```

### Step 3 — Verify the institution
The satellite view showed the football ground situated within a university campus. Surrounding map labels and campus infrastructure confirmed the site belongs to **Baba Ghulam Shah Badshah University (BGSBU)**, Rajouri, Jammu & Kashmir — consistent with the challenge's description of a university in a northern Indian Union Territory.

## 5. Evidence Summary

| Field | Value |
|---|---|
| Coordinates | 33.3960° N, 74.3448° E |
| Institution | Baba Ghulam Shah Badshah University (BGSBU) |
| Location | Rajouri, Jammu & Kashmir |

## 6. Conclusion

The identification relied on comparing the temporal change in satellite imagery (bare clearing → completed ground) against the stated geographic constraint, then confirming the site through map labeling of the surrounding campus. The result is independently reproducible by viewing historical imagery at the given coordinates.

## 7. Flag

```
FLAG{33.3960,74.3448}
```
