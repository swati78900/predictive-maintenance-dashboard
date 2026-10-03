# predictive-maintenance-dashboard                      
# AI/ML‑Based Predictive Maintenance & Downtime Risk Monitoring Dashboard


## Problem
In FMCG manufacturing, unexpected machine breakdowns cause unplanned downtime, production loss, and delays in meeting the production plan. This impacts dispatch reliability (OTIF) and increases maintenance cost.

## Solution
Built an ML-driven predictive maintenance system that predicts **machine failure probability** using operating conditions and converts it into:
- **Risk Bands (Low/Medium/High)**
- **Early Warning alerts**
- **Maintenance Priority Queue**
- **Dashboard for plant/asset monitoring**
- **Assumption-based downtime & cost impact simulation (Excel)**

## Dataset
Model: Random Forest | PR-AUC: 0.857 | Threshold: 0.35
Dashboard pages: Plant Overview, Asset Performance, Early Warning Queue, Failure Drivers, Downtime & Cost Impact
AI4I 2020 Predictive Maintenance Dataset (10,000 rows, 14 columns).
Target: `Machine failure` (0/1)

Key inputs used (leakage-free):
- Type
- Air temperature [K]
- Process temperature [K]
- Rotational speed [rpm]
- Torque [Nm]
- Tool wear [min]
- Engineered: Temp_diff = Process - Air temperature

Excluded from training to prevent target leakage:
- TWF, HDF, PWF, OSF, RNF (failure mode outcomes)

## Data Quality Check
Detected 27 inconsistent records between the main failure label and failure-mode flags:
- Modes=1 but failure=0: 18
- Failure=1 but modes=0: 9
Flagged as data-quality exceptions; used consistent subset for modeling.

## Model
Compared baseline Logistic Regression vs Random Forest.
Final model: **Random Forest Classifier**
- PR-AUC: ~0.857 (imbalanced classification)
- Tuned threshold: 0.35 for early warning (precision/recall trade-off)

Top drivers (feature importance):
- Torque, Rotational speed, Tool wear, Temp_diff

## Dashboard (Power BI)
Pages:
1. Plant Overview (KPIs, risk distribution, failure causes)
2. Asset Performance (Top risky assets)
3. Early Warning Queue (maintenance priority list + action recommended)
4. Failure Drivers (feature importance)
5. Downtime & Cost Impact (assumption-based simulation)

## Business Impact (Simulation)
Excel-based scenario model estimates:
- Total expected downtime avoided (hrs)
- Total expected cost avoided
(Assumptions documented in `Maintenance_Simulation_FINAL.xlsx`)

## Files
- Power BI report: `powerbi/HUL_PredictiveMaintenance.pbix`
- Excel simulation: `excel/Maintenance_Simulation_FINAL.xlsx`
- Screenshots: `screenshots/`
