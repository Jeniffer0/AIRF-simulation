# AIRF Simulation Code
## Actuarial Design of a Continental Insurer Resolution Facility for Africa (AIRF)
### A Compound Poisson Excess-of-Loss Model

**Author:** Atetwe Jeniffer Nasike  
**Manuscript:** EUAJ-D-26-00062-R1 | *European Actuarial Journal*  
**Contact:** jeniffernasike@gmail.com

---

## What this repository contains

| File | Description |
|------|-------------|
| `AIRF_simulation_VERIFIED.R` | Main R simulation script — fully documented, all results reproducible |
| `README.md` | This file |

---

## Data source

All calibration inputs come from publicly available IRA Kenya data:

**Insurance Regulatory Authority Kenya (IRA Kenya)**  
Annual Insurance Industry Statistics 2023 & 2024  
https://www.ira.go.ke/index.php/publications/statistics

Key appendices used:
- **Appendix 1** — Insurance Revenue (GEP) by company, 2024
- **Appendix 6 I–IV** — Balance sheets (Insurance Contract Liabilities) by company, 2024
- **Appendix 45 & 46** — Motor death claim counts and amounts, 2023
- **Appendix 51 & 52** — Motor death claim counts and amounts, 2024

---

## Verified calibration inputs

| Parameter | Value from real data | Paper citation |
|-----------|---------------------|----------------|
| Total GEP (insurers, 2024) | KSh 201,422 million | Section 4.5 |
| ICL companies with ICL > 0 | 33 | Section 3.3 |
| Mean ICL | KSh 4,865 million | Section 3.3 |
| Empirical CV of ICL | 0.780 | Section 3.3 |
| Min ICL (Corporate Insurance) | KSh 397.6 million | Section 3.3 |
| Max ICL (GA Insurance) | KSh 15,417 million | Section 3.3 |
| Total ICL | KSh 160,552 million | Section 3.3 |
| Mean motor death claim, 2024 | KSh 793,084 | Section 3.2 |
| Motor death claims settled, 2024 | 3,598 | Table 4 |
| 75th percentile company means, 2024 | KSh 1,372,424 | Table 4 |
| Mean motor death claim, 2023 | KSh 697,557 | Table 4 |
| Motor death claims settled, 2023 | 2,675 | Table 4 |

---

## How to run

### Requirements
```r
# Base R (>= 4.0) — no external packages needed for the simulation
# Optional: readxl for Section 0 (direct data extraction from Excel)
install.packages("readxl")  # optional only
```

### Run simulation
```r
source("AIRF_simulation_VERIFIED.R")
```

All output is printed to console. Fixed seed 2026 ensures full reproducibility.

### Run on GitHub Actions (CI)
The script runs in base R with no dependencies. Add this `.github/workflows/simulate.yml`:

```yaml
name: AIRF Simulation
on: [push, pull_request]
jobs:
  simulate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: r-lib/actions/setup-r@v2
        with:
          r-version: '4.3'
      - name: Run simulation
        run: Rscript AIRF_simulation_VERIFIED.R
```

### Read directly from IRA Excel files
```r
# Download IRA data from https://www.ira.go.ke/index.php/publications/statistics
# then run:
install.packages("readxl")
ira <- extract_IRA_data(
  path_2023 = "IRA_Kenya_Annual_Statistics_2023.xlsx",
  path_2024 = "IRA_Kenya_Annual_Statistics_2024.xlsx"
)
```

---

## Key results (from simulation, seed 2026)

| Quantity | Value |
|----------|-------|
| E[Y(i)] per country per year | KSh ~268 million (USD ~2.1 million) |
| E[Y_pool] (8 countries) | USD ~16 million per year |
| VaR(99.5%) — Solvency II benchmark | USD ~193 million |
| Solvency probability (USD 200m capital) | ~99.55% |
| Annual premium per country | USD ~2.0–2.5 million |

---

## Citation

```
Atetwe, J.N. (2026). Actuarial Design of a Continental Insurer Resolution 
Facility for Africa (AIRF): A Compound Poisson Excess-of-Loss Model.
European Actuarial Journal. Manuscript EUAJ-D-26-00062-R1.
```

---

## Can R run on GitHub?

Yes — GitHub Actions supports R natively via `r-lib/actions/setup-r`. 
The simulation script has **zero external dependencies** (uses only base R), 
so it runs cleanly on any standard R installation including the GitHub 
Actions Ubuntu runner. See the workflow YAML above.
