# nb-demand-supply-stress-model
Demand–supply stress indicators, capacity risk signals, and economic sensitivity analysis for Malaysia’s electricity grid using public TNB and IPI data.
# Malaysia Electricity Demand–Supply Stress Modeling

This project builds explainable indicators to quantify **demand–supply stress** and **capacity risk** for Malaysia’s electricity system using monthly public datasets. The core output includes a demand–supply ratio, a reserve margin proxy, and a z-score based stress index. The project also includes an optional economic sensitivity layer using the Industrial Production Index (IPI), seasonally adjusted.

## Objectives
1. Build simple, defensible indicators that summarize capacity risk in a planning-friendly way.
2. Identify **high-stress months** and recurring seasonal patterns.
3. Evaluate how industrial activity (IPI) relates to electricity demand and stress.
4. (Optional) Forecast demand and translate forecasts into future stress/risk signals under supply scenarios.

## Data
Input CSV files:
- `electricity_supply_clean.csv` (columns: `date`, `sector`, `supply`)
- `electricity_consumption_clean.csv` (columns: `date`, `sector`, `consumption`)
- `ipi_clean.csv` (columns: `series`, `date`, `index`, `index_sa`)

Recommended usage:
- Start with `sector = total` for both supply and consumption.
- For IPI, use `series = abs` and `index_sa` (seasonally adjusted) for the cleanest economic signal.

Data sources:
- Tenaga Nasional Berhad (via Malaysia open data portal)
- Department of Statistics Malaysia (IPI, via Malaysia open data portal)

## Methods and Indicators
### 1) Demand–Supply Ratio
Measures how closely demand approaches supply.
- `ratio = consumption / supply`

### 2) Reserve Margin Proxy
A simple “headroom” proxy (higher is safer).
- `reserve = 1 - ratio`

### 3) Stress Index (z-score on the ratio)
Highlights unusually high stress relative to historical baseline.
- `stress = (ratio - mean(ratio)) / std(ratio)`

### 4) Explainable Anomaly Detection
For utility planning contexts, explainable rules are often preferred:
- thresholding on `stress` (e.g., `stress > 2`)
- rolling z-score 

### 5) Economic Sensitivity (IPI)
Quantifies relationships between industrial activity and electricity demand/stress:
- correlation between `ΔIPI` and `Δconsumption` or `Δratio`
- lag testing (1–3 months) to explore leading/lagging behavior

## Repository Structure
.
├─ data/
│ ├─ raw/ # optional: raw source files
│ └─ processed/ # cleaned + featured datasets
├─ notebooks/
│ ├─ 01_data_validation.ipynb
│ ├─ 02_stress_indicators.ipynb
│ ├─ 03_ipi_sensitivity.ipynb
│ └─ 04_forecasting_optional.ipynb
├─ src/
│ ├─ build_dataset.py # merge + feature engineering
│ ├─ metrics.py # indicator formulas
│ └─ utils.py
├─ reports/
│ ├─ executive_summary.md
│ └─ figures/
├─ requirements.txt
└─ README.md
