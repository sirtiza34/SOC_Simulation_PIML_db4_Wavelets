# SOC_Simulation_PIML_db4_Wavelets
Soil Organic Carbon (SOC) simulation under Shared Socioeconomic Pathways (SSP126, SSP245, SSP370 &amp; SSP585) using XGBoost-based Physics-informed Machine Learning (PIML) and Daubechies-4 wavelet decomposition.

## Repository Overview

This repository contains Python scripts used to simulate and analyse future trajectories of $SOC_{stock}$ using a PIML framework combined with wavelet-based time-series analysis.

The workflow consists of three major components:

1. **Dataset Construction**
   - Spatial datasets (soil, land use, and climate variables) are integrated from multiple sources including LUH2 land-use projections and bias-corrected climate model outputs.
   - Multi-model ensemble climate variables are aggregated seasonally and annually.
   - Baseline and future datasets are generated for each grid cell using rolling temporal windows.

2. **PIML Modelling and Simulation**
   - $SOC_{stock}$ is modelled using XGBoost regression with monotonic constraints representing known soil–climate relationships.
   - Bias correction is applied using smearing estimators and national $SOC_{stock}$ anchoring.
   - Ensemble modelling and quantile regression are used to quantify predictive uncertainty.
   - Model explainability is analysed using SHAP values.

3. **$SOC_{stock}$ Projection and Temporal Analysis**
   - The trained PIML model is used to generate $SOC_{stock}$ projections for SSP126, SSP245, SSP370, and SSP585 scenarios.
   - Time-series signals are decomposed using Daubechies-4 wavelet decomposition.
   - Long-term $SOC_{stock}$ trends are analysed using Mann–Kendall tests, Sen’s slope, generalized additive models (GAM), and breakpoint detection.

The scripts also generate all tables and figures used in the analysis, including uncertainty diagnostics, SHAP feature importance, and wavelet-derived trend trajectories.

## Scripts / Notebooks

### `S1_PIML_Modelling.ipynb`

Builds the PIML model for $SOC_{stock}$ prediction.  
The script:

- constructs baseline and future predictor datasets
- trains constrained and unconstrained XGBoost models
- applies bias correction and anchoring to match national $SOC_{stock}$ totals
- quantifies prediction uncertainty using ensemble and quantile models
- generates $SOC_{stock}$ projections for SSP scenarios
- produces diagnostic plots, SHAP analysis, and learning curves

---

### `S2_Wavelet_Approximation.ipynb`

Performs wavelet-based analysis of projected $SOC_{stock}$ trajectories.  
The script:

- decomposes $SOC_{stock}$ time series using Daubechies-4 wavelets
- extracts low-frequency $SOC_{stock}$ trend signals (A3 and A5 approximations)
- detects structural breakpoints using the PELT algorithm
- evaluates trend significance using Mann–Kendall tests and Sen’s slope
- fits GAM smoothers to compare long-term trajectories
- analyses regime-wise $SOC_{stock}$ sequestration rates
- generates visualisations and statistical summaries of $SOC_{stock}$ trends.
