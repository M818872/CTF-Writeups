# Proof of Concept: The Silent Transfer

| Field | Detail |
|---|---|
| Challenge | The Silent Transfer |
| Category | OSINT / Digital Forensics |
| Points | 30 |
| Evidence | `Case Files.zip` |
| Status | Solved |

## 1. Scenario

A company reported a suspected unauthorized data transfer from its internal server. Multiple employees had accessed and downloaded files from the server around the time of the incident, so the responsible party could not be determined from a single log.

## 2. Objective

Identify the specific employee and device responsible for the suspicious data transfer.

## 3. Methodology

Correlation across four independent data sources, rather than reliance on any single log:

- IPDR / gateway records (network transfer volume and timing)
- Wi-Fi controller logs (IP-to-MAC mapping)
- Employee device inventory (MAC-to-employee mapping)
- Server access logs (independent corroboration of user activity)

## 4. Investigation Steps

### Step 1 — Identify the anomalous network session
Review of the IPDR/gateway records identified one outlier session:

| Field | Value |
|---|---|
| Date | 2026-09-05 |
| Time | ~22:14 – 22:46 |
| Data volume | ~10.47 GB (downlink) |
| Internal IP | 10.20.14.119 |
| Corporate server | 54.212.34.101 |

This volume was far larger than any other session in the dataset, making it the primary candidate.

### Step 2 — Map the IP to a device
Wi-Fi controller logs for the same window mapped internal IP `10.20.14.119` to MAC address `3C:52:82:4B:91:2A`, connected via the `CORP-WIFI` network.

### Step 3 — Identify the employee
The employee device inventory mapped that MAC address to:

| Field | Value |
|---|---|
| Employee ID | EMP-019 |
| Employee | Rohan Deshmukh |
| Device | ENG-NB-19 |
| Model | Dell Latitude 7440 |

### Step 4 — Corroborate with server logs
Server access logs for 5 September showed the same user account downloading several large archives during the relevant window: `project_delta_snapshot.tar.gz`, `quarterly_export.zip`, `q3_release_bundle.tar.gz`. This independently corroborates the network-layer finding.

## 5. Evidence Summary

| Source | Finding |
|---|---|
| IPDR | ~10.47 GB transfer, IP 10.20.14.119, 2026-09-05 ~22:14–22:46 |
| Wi-Fi controller | IP 10.20.14.119 → MAC 3C:52:82:4B:91:2A |
| Device inventory | MAC 3C:52:82:4B:91:2A → EMP-019, Rohan Deshmukh, ENG-NB-19 |
| Server logs | Same user downloaded 3 large archives on 5 Sept, matching the transfer window |

## 6. Conclusion

No single log conclusively identified the responsible party — the initial IPDR anomaly could only be attributed to a specific device via Wi-Fi logs, and to a specific employee via the device inventory. Server access logs then independently confirmed the same user's activity during the matching time window, giving four-way corroboration rather than a single point of failure.

## 7. Flag

```
FLAG{ROHAN_3C:52:82:4B:91:2A}
```
