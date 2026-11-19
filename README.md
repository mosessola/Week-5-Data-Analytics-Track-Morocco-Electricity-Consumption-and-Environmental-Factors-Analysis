# Week 5 – Data Analytics Track: Morocco Electricity Consumption and Environmental Factors Analysis

AnalystLab Africa – Experience Lab Internship Programme. Exploratory analysis and visualisation of electricity consumption in three zones (10-minute readings, 1 Jan – 30 Dec 2017) with temperature, humidity and wind speed.

> The interactive dashboard is **not** part of this submission; it will be added separately.

## Folder contents
| Path | Description |
|---|---|
| `Morocco_Electricity_Analysis.ipynb` | Main notebook (Tasks 1–6), already executed |
| `Morocco_Electricity_Analytical_Report.pdf` | Short analytical report |
| `data/powerconsumption_cleaned.csv` | Cleaned input dataset |
| `data/powerconsumption_datadictionary.csv` | Data dictionary |
| `data/powerconsumption_prepared.csv` | Output of the preparation steps (time features, total demand, energy per interval) |
| `charts/static/` | 10 Matplotlib/Seaborn charts (PNG) |
| `charts/interactive/` | 7 interactive Plotly charts (standalone HTML, open in a browser) |
| `results.json` | Key figures written by the notebook and used in the report |
| `requirements.txt` | Python packages |

## How to reproduce
1. Install Python 3.10+ and create an environment (optional): `python -m venv venv`, then activate it.
2. Install packages: `pip install -r requirements.txt`
3. Open a terminal in this folder and run: `jupyter notebook Morocco_Electricity_Analysis.ipynb` (or JupyterLab / VS Code).
4. Run all cells top to bottom (Kernel > Restart & Run All). Charts and `results.json` are regenerated; paths are relative, so run from this folder.

## Key interpretation decisions (please read)
- **Unit of consumption:** the dictionary says kWh, but the magnitudes only make sense as average power (**kW**) per 10-minute interval. Readings are therefore **not summed as energy**; energy is computed as kW × 10/60 h. This is an assumption and should be confirmed.
- **GeneralDiffuseFlows / DiffuseFlows:** described as gas-emission diffusion, but the data are ~0 at night and peak at midday, like solar radiation. They are treated as solar-radiation-like context variables only.
- **Extreme values:** Zone 3's high readings are consistent summer-evening peaks (not errors) and were kept.
- **Coverage:** 31 Dec 2017 is absent, so the data hold 364 days. Correlations are associations, not causation.
