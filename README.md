# 🌌 Starlink Regional Pricing Optimization — Nevada, Nebraska, and Iowa

### Objective
Determine the **optimal residential pricing strategy** for Starlink service across **Nevada, Nebraska, and Iowa** to **maximize customer adoption** while **maintaining average revenue per user (ARPU)**.

This project uses **publicly available data** to model broadband competition, identify underserved markets, and estimate the adoption response to different pricing tiers.

---

## 🧭 Project Overview

| Stage | Description |
|-------|--------------|
| **1. Problem Definition** | Define objective, constraints, and KPIs — maximize adoption while preserving ARPU. |
| **2. Data Collection** | Pull public data (FCC Broadband Map, ACS Census API, BroadbandNow, Ookla) for the three states. |
| **3. Exploratory Analysis** | Assess competition, coverage gaps, demographics, and rurality via visualizations. |
| **4. Modeling** | Estimate adoption response (logit model) and solve for prices that meet the ARPU constraint. |
| **5. Optimization** | Run grid search / solver to identify price levels maximizing adoption given ARPU bounds. |
| **6. Results & Insights** | Visualize adoption vs. price trade-offs and present pricing recommendations. |

---

## 📂 Repository Structure

starlink-pricing/
├─ README.md                # Project overview, data sources, and methodology
├─ research.ipynb           # Main notebook with EDA, modeling, and results
├─ model.py                 # Optimization model (price elasticity + ARPU constraint)
├─ data/
│  ├─ raw/                  # Raw FCC, Census, and BroadbandNow datasets
│  ├─ interim/              # Cleaned + joined county-level data
│  └─ external/             # Static reference data (e.g., FIPS codes)
├─ src/
│  ├─ fetch_census.py       # Pulls ACS demographic & internet subscription data
│  ├─ fetch_fcc_bdc.md      # Documentation for downloading BDC bulk data
│  ├─ clean_join.py         # Cleans, merges, and enriches data sources
│  ├─ price_model.py        # Defines price-response and optimization functions
│  └─ viz.py                # Generates key plots and maps
├─ config/
│  └─ variables.yaml        # Table IDs, FIPS codes, and model parameters
└─ environment.yml          # Conda environment (Python, pandas, geopandas, etc.)

---

## Data Sources

| Dataset | Description | Source |
|----------|--------------|--------|
| **FCC Broadband Data Collection (BDC)** | Broadband availability & provider counts by technology | [FCC National Broadband Map](https://broadbandmap.fcc.gov/home) |
| **American Community Survey (ACS)** | Demographics, income, rurality, and subscription data | [Census API (2023 1-Year)](https://www.census.gov/data/developers/data-sets/acs-1year.html) |
| **BroadbandNow** | Provider pricing snapshots and plan ranges | [BroadbandNow.com](https://broadbandnow.com/) |
| **Ookla Speedtest Intelligence** | Average speed benchmarks (for validation only) | [Ookla Global Index](https://www.speedtest.net/global-index) |
| **Starlink Official Plans** | Baseline prices and plan definitions | [Starlink.com](https://www.starlink.com/) |

---

## Methodology

1. **Data Aggregation**
   - Merge county-level FCC and ACS data to identify underserved households.
   - Derive key variables: provider count, median income, population density, % rural, and internet subscription rate.

2. **Modeling Adoption**
   - Estimate potential adoption share using a **logit demand model** with **price**, **income**, and **competition** features.
   - Calibrate elasticity to match broadband studies (baseline −0.45).

3. **Optimization**
   - Maximize total projected adoption `Σ adoption(price) × households`
   - Subject to ARPU ≥ baseline constraint.
   - Perform state-level and two-tier (Lite / Residential) scenarios.

4. **Scenario Analysis**
   - Simulate impact of discounting in low-competition counties.
   - Visualize adoption curves and price–ARPU trade-offs.

---

## Brief Results Overview
- **Optimal price bands** by state and service tier.  
- **Projected adoption uplift** vs. current pricing.  
- **ARPU trade-off analysis** showing feasible price corridors.  
- **Policy & expansion implications** — where lower pricing yields the strongest ROI on coverage.

---

## Recommendations & Next Steps
- Integrate tract-level granularity to improve rural targeting.  
- Add sensitivity analysis for different elasticity priors (−0.3 to −0.7).  
- Simulate multi-tier regional pricing (e.g., metro vs. rural discounting).  
- Extend to neighboring states for cross-border adoption spillovers.

---

All data used is **publicly available**; no proprietary datasets are accessed.

---