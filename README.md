# AURN Air Quality Imputation — IJC319 Digital Artefact

**Title:** Evaluating Traditional, Machine Learning, and Generative AI-Based Methods for Imputing Missing Values in AURN Air Quality Data for Greater London

**Author:** Tun Muhammad Hariz Bin Tun Mahadi
**Supervisor:** Asra Aslam
**University:** University of Sheffield
**Module:** IJC319 — Responsible Data Science Lab 2

---

## Project Overview

This repository contains the full Python-based imputation benchmarking pipeline developed as the digital artefact for the IJC319 dissertation. The project evaluates six imputation methods across three methodological tiers on hourly AURN air quality data for Greater London (2024) under a Missing Not at Random (MNAR) missingness mechanism.

The six methods benchmarked are:

| Tier | Method |
|------|--------|
| Traditional Statistical | Mean Imputation, Linear Regression (OLS) |
| Machine Learning | k-Nearest Neighbour (KNN), Random Forest (MissForest) |
| Generative AI | Autoencoder, GAIN (Generative Adversarial Imputation Network) |

Performance is evaluated using RMSE, MAE, and R² across five pollutants: NO₂, O₃, PM10, PM2.5, and SO₂.

---

## Research Questions

**RQ1:** How effectively can different imputation methods — spanning traditional statistical, machine learning, and generative AI approaches — reconstruct missing pollutant concentration values in AURN data across different pollutant types, and which technique provides the most accurate reconstruction?

**RQ2:** Do advanced machine learning and generative AI models outperform traditional statistical methods in recovering missing pollutant values, or does the structure of the dataset favour simpler, well-specified approaches?

---

## Hypotheses

**H1:** Machine learning methods will achieve lower error rates (RMSE, MAE) and higher predictive accuracy (R²) than traditional statistical methods under the MNAR mechanism, owing to their capacity to exploit non-linear inter-pollutant dependencies.

**H2:** Generative AI methods will not outperform machine learning methods under the MNAR mechanism at this dataset scale, with GAIN's adversarial convergence expected to be constrained by the limited number of training observations relative to Random Forest's ensemble stability.

**H3:** Sulphur dioxide will prove significantly more resistant to imputation than other pollutants across all methods, owing to its weak correlations with co-measured pollutants.

---

## Methodology

### Research Design
This study adopts a deductive, quantitative research design. Artificial missingness is introduced into a complete ground-truth dataset, enabling evaluation of imputation accuracy against known held-out values using standardised error metrics (RMSE, MAE, R²).

### Pipeline Overview

The pipeline is structured into three main steps:

**Step 1 — Data Preparation**
- Dataset sourced from the UK AURN via the official Government air quality portal
- Covers hourly pollutant measurements from a single Greater London station across the full year 2024 (8,784 hourly observations)
- Rows with pre-existing missing values removed, yielding a clean ground-truth dataset of 7,315 observations
- Pollutants included: NO₂, O₃, PM10, PM2.5, SO₂

**Step 2 — Missingness Simulation**
- Artificial MNAR-like missingness introduced using the `mdatagen` library
- 70% of missing values deterministically concentrated at the highest-concentration observations (randomness parameter = 0.3), consistent with real AURN sensor dropout patterns
- ~5% missingness rate applied uniformly across all five pollutants
- Masked values held out exclusively for evaluation (no information leakage)

**Step 3 — Imputation and Evaluation**
- All six methods applied independently to the dataset with artificial missingness
- Performance evaluated by comparing imputed values against held-out ground truth
- Three complementary metrics computed per method–pollutant combination:
  - **RMSE** — penalises large errors, sensitive to extreme imputation failures
  - **MAE** — average error in original pollutant units (μg/m³)
  - **R²** — proportion of true variance explained (negative values indicate worse than mean baseline)

---

## Repository Contents

| File | Description |
|------|-------------|
| `AURN_Imputation_Pipeline.ipynb` | Main notebook — full pipeline from data loading to results visualisation |
| `Greater_London.csv` | AURN hourly air quality dataset for Greater London, full year 2024 |
| `README.md` | This file |

---

## How to Run (Google Colab)

1. Go to [colab.research.google.com](https://colab.research.google.com)
2. Click **File → Upload notebook**
3. Upload `AURN_Imputation_Pipeline.ipynb`
4. Upload `Greater_London.csv` to the Colab session files (click the folder icon on the left sidebar → upload)
5. Run all cells from top to bottom (**Runtime → Run all**)

---

## Pipeline Structure

The notebook is organised into seven steps matching the dissertation methodology:

| Step | Section | Description |
|------|---------|-------------|
| Step 0 | — | Import libraries |
| Step 1 | Section 3.1 Step 1 | Data loading, cleaning, ground-truth creation |
| Step 2 | Section 3.1 EDA | Descriptive statistics and Pearson correlation (Figure 3) |
| Step 3 | Section 3.1 Step 2 | MNAR missingness simulation using `mdatagen` (Figure 2) |
| Step 4 | Section 3.1 Methods | Six imputation methods applied in order |
| Step 5 | Section 3.1 Step 3 | Evaluation — RMSE, MAE, R² computation |
| Step 6 | Section 4 | Results visualisation — all dissertation figures (Figures 4–11) |
| Step 7 | Appendix | Supplementary visualisations |

---

## Dependencies

All dependencies are installed automatically by the first cell of the notebook. The key libraries used are:

- `mdatagen` — MNAR missingness simulation
- `pandas`, `numpy` — data handling
- `scikit-learn` — Mean, KNN, Regression, Random Forest imputation and metrics
- `tensorflow` / `keras` — Autoencoder and GAIN implementation
- `matplotlib`, `seaborn` — visualisation

---

## Key Results

Random Forest and GAIN jointly emerged as the strongest performers:

- **Random Forest** achieved the lowest RMSE for NO₂, ozone, and PM2.5
- **GAIN** achieved the lowest MAE for ozone, PM10, and SO₂
- Both methods substantially outperformed Mean, KNN, Regression, and Autoencoder
- Five positive R² values recorded: ozone under GAIN (0.341) and Random Forest (0.226), PM10 under GAIN (0.231), PM2.5 under Random Forest (0.303) and GAIN (0.068)
- Sulphur dioxide proved uniformly resistant across all methods due to weak inter-pollutant correlations
- H1 supported, H2 rejected, H3 confirmed

---

## Dataset

The dataset `Greater_London.csv` contains hourly pollutant measurements from a Greater London AURN monitoring station across the full year 2024, obtained from the UK Air Quality Data Portal.

**Source:** [https://www.get-air-pollution-data.service.gov.uk](https://www.get-air-pollution-data.service.gov.uk)

**Pollutants:** NO₂, O₃, PM10, PM2.5, SO₂

The raw dataset contains 8,784 hourly observations. After removing rows with pre-existing missing values, the clean ground-truth dataset contains **7,315 observations**.

---

## Ethical Approval

This research relies exclusively on publicly available AURN records published by DEFRA. The data contains no personally identifiable information. Ethical approval was granted by the University of Sheffield Research Ethics Committee (Reference: 071604, approved 13/11/2025).

---

## Licence

This project is submitted as academic coursework at the University of Sheffield. All code is original unless otherwise cited in the dissertation.
