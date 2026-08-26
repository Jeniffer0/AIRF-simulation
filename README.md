# AIRF Simulation Code

## Actuarial Design of a Continental Insurer Resolution Facility for Africa (AIRF)
### A Compound Poisson Excess-of-Loss Model

**Author:** Jeniffer Nasike Atetwe  
**Manuscript:** EUAJ-D-26-00062-R1 | *European Actuarial Journal*  
**Contact:** jeniffernasike@gmail.com

[![AIRF Simulation](https://github.com/jeniffernasike/AIRF-simulation/actions/workflows/simulate.yml/badge.svg)](https://github.com/jeniffernasike/AIRF-simulation/actions/workflows/simulate.yml)

---

## Repository structure

```
AIRF-simulation/
├── AIRF_simulation_VERIFIED.R   ← Main simulation script
├── README.md                    ← This file
├── data/
│   ├── IRA_Kenya_Annual_Statistics_2023.xlsx   ← Source data
│   └── IRA_Kenya_Annual_Statistics_2024.xlsx   ← Source data
└── .github/
    └── workflows/
        └── simulate.yml         ← GitHub Actions (auto-runs on every commit)
```

---

## Data source

**Insurance Regulatory Authority Kenya (IRA Kenya)**  
Annual Insurance Industry Statistics 2023 & 2024  
https://www.ira.go.ke/index.php/publications/statistics

Key appendices:

| Appendix | Content | Year |
|----------|---------|------|
| Appendix 1 | Insurance Revenue (GEP) by company | 2024 |
| Appendix 6 I–IV | Balance sheets — Insurance Contract Liabilities | 2024 |
| Appendix 45 & 46 | Motor death claim counts and amounts | 2023 |
| Appendix 51 & 52 | Motor death claim counts and amounts | 2024 |

---

## Verified calibration inputs (all match paper exactly)

| Parameter | Real data value | Paper citation |
|-----------|----------------|----------------|
| Total GEP (insurers, 2024) | KSh 201,422 million ✓ | Section 4.5 |
| ICL companies with ICL > 0 | 33 ✓ | Section 3.3 |
| Mean ICL | KSh 4,865 million ✓ | Section 3.3 |
| Empirical CV of ICL | 0.780 ✓ | Section 3.3 |
| Min ICL (Corporate Insurance) | KSh 397.6 million ✓ | Section 3.3 |
| Max ICL (GA Insurance) | KSh 15,417 million ✓ | Section 3.3 |
| Total ICL | KSh 160,552 million ✓ | Section 3.3 |
| Mean motor death claim 2024 | KSh 793,084 ✓ | Table 4 |
| Motor death claims settled 2024 | 3,598 ✓ | Table 4 |
| 75th percentile (company means) 2024 | KSh 1,372,424 ✓ | Table 4 |
| Mean motor death claim 2023 | KSh 697,557 ✓ | Table 4 |
| Motor death claims settled 2023 | 2,675 ✓ | Table 4 |

---

## Key simulation results

| Quantity | Value | Paper |
|----------|-------|-------|
| E[Y(i)] per country per year | KSh ~268m (USD ~2.1m) | Section 5 |
| E[Y_pool] (8 countries) | USD ~16m/year | Table 3 |
| VaR(99.5%) — Solvency II | USD ~193 million | Table 3 |
| Solvency at USD 200m capital | ~99.55% | Table 3 |
| Annual premium per country | USD ~2.0–2.5 million | Table 3 |

---

## How to run

### Option 1 — Run locally (R required)
```r
# No packages needed — base R only
# (readxl optional, for Section 0 data verification from Excel)
source("AIRF_simulation_VERIFIED.R")
```

### Option 2 — GitHub Actions (runs automatically)
Every time you push a commit, GitHub runs the simulation automatically.  
Check the **Actions** tab to see the results.

---

## Citation

```
Atetwe, J.N. (2026). Actuarial Design of a Continental Insurer Resolution
Facility for Africa (AIRF): A Compound Poisson Excess-of-Loss Model.
European Actuarial Journal. Manuscript EUAJ-D-26-00062-R1.
```
