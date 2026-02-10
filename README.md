# Malaysia Electricity Demand–Supply Stress Modeling

This repository builds explainable indicators to quantify **demand–supply stress** and **capacity risk** for Malaysia’s electricity system using monthly public datasets. Core outputs include a demand–supply ratio, a reserve margin proxy, and a z-score based stress index. The project also evaluates economic sensitivity using the **Industrial Production Index (IPI)** (seasonally adjusted).

## Project Goals
- Build defensible indicators that summarize grid capacity risk from monthly demand and supply data.
- Identify high-stress months and recurring seasonal patterns.
- Quantify the relationship between industrial activity (IPI) and electricity demand/stress.
- Provide a clean, reproducible workflow suitable for review and portfolio evaluation.

## Data Sources and Licensing
This project uses public datasets licensed under **Creative Commons Attribution 4.0 (CC BY 4.0)**. Attribution is provided below.

- Electricity supply and electricity consumption datasets: published on Malaysia’s open data portal by Tenaga Nasional Berhad (TNB).  
  Source: https://data.gov.my/
- Industrial Production Index (IPI): published by the Department of Statistics Malaysia (DOSM) on OpenDOSM.  
  Source: https://open.dosm.gov.my/

Data in `data/processed/` is derived from these sources and is redistributed with attribution under CC BY 4.0.

## Repository Structure
```text
.
├─ data/
│  └─ processed/
│     ├─ electricity_supply_clean.csv
│     ├─ electricity_consumption_clean.csv
│     └─ ipi_clean.csv
├─ notebooks/
│  ├─ 01_data_validation.ipynb
│  ├─ 02_stress_indicators.ipynb
│  ├─ 03_ipi_sensitivity.ipynb
│  └─ 04_forecasting.ipynb
├─ reports/
│  ├─ executive_summary.md
│  └─ figures/
├─ src/
│  ├─ build_dataset.py
│  ├─ metrics.py
│  └─ utils.py
├─ requirements.txt
├─ LICENSE
└─ README.md

```
# Environment Setup
## 1) Clone the repository
-git clone <REPO_URL>
-cd <REPO_FOLDER>

## 2) Create and activate a virtual environment
python -m venv .venv


## Windows (PowerShell)

.venv\Scripts\Activate.ps1


## Windows (cmd)

.venv\Scripts\activate.bat


## Mac/Linux

source .venv/bin/activate

3) Install dependencies
pip install --upgrade pip
pip install -r requirements.txt

## 4) Launch Jupyter
jupyter notebook

## How to Run (Notebook Workflow)

Run notebooks in the following order:

notebooks/01_data_validation.ipynb
Validates schema and date continuity, filters to sector = total, and produces a merged dataset.

notebooks/02_stress_indicators.ipynb
Builds stress indicators, outputs rankings of high-stress months, and saves figures to reports/figures/.

notebooks/03_ipi_sensitivity.ipynb
Filters IPI to series = abs, uses index_sa (seasonally adjusted), and performs correlation and lag checks.

notebooks/04_forecasting.ipynb
Forecasts electricity demand (consumption) and translates forecasts into stress signals under a baseline supply assumption.

## Indicators

Indicators are computed on monthly totals (sector = total).

Demand–Supply Ratio
ratio = consumption / supply

Reserve Margin Proxy
reserve = 1 - ratio

Stress Index (z-score on ratio)
stress = (ratio - mean(ratio)) / std(ratio)

## Outputs

Outputs are written to:

data/processed/ for featured datasets

reports/figures/ for charts

reports/executive_summary.md for a one-page summary

Primary outputs include:

a featured dataset containing ratio, reserve, and stress

a ranking table of high-stress months

time-series figures for demand, supply, and stress

economic sensitivity results using seasonally adjusted IPI

## Notes on Reproducibility

The repository includes cleaned, processed datasets in data/processed/ to allow immediate execution.

The analysis depends on the dataset definitions published by the providers.

All derived metrics are computed using transparent formulas listed in this README.

## License

Code in this repository is licensed under the MIT License (see LICENSE).
Datasets are licensed under CC BY 4.0 by their respective publishers; this repository redistributes derived processed data with attribution as stated above.

## Contact

Ameer Syahiran Azhan
LinkedIn: https://www.linkedin.com/in/ameer-syahiran-azhan-7bb898238
