# AURN Air Quality Imputation — IJC319 Digital Artefact

**Title:** Evaluating Traditional, Machine Learning, and Generative AI-Based Methods for Imputing Missing Values in AURN Air Quality Data for Greater London

**Author:** Tun Muhammad Hariz Bin Tun Mahadi
**Registration Number:** 230190355
**Supervisor:** Asra Aslam
**University:** University of Sheffield
**Module:** IJC319 — Responsible Data Science Lab 2

---

## Project Overview

This repository contains the full Python-based imputation benchmarking pipeline developed as the digital artefact for the IJC319 dissertation. The project evaluates six imputation methods across three methodological tiers on hourly AURN air quality data for Greater London (2024) under a Missing Not at Random (MNAR) missingness mechanism.

The six methods benchmarked are:

| Tier | Method |
|------|--------|
| Traditional Statistical | Mean Imputation, Linear Regression |
| Machine Learning | k-Nearest Neighbour (KNN), Random Forest (MissForest) |
| Generative AI | Autoencoder, GAIN (Generative Adversarial Imputation Network) |

Performance is evaluated using RMSE, MAE, and R² across five pollutants: NO₂, O₃, PM10, PM2.5, and SO₂.

---

## Repository Contents

| File | Description |
|------|-------------|
| `AURN_Imputation_Pipeline.ipynb` | Main notebook — full pipeline from data loading to results visualisation |
| `Greater_London.csv` | AURN hourly air quality dataset for Greater London, full year 2024 |
| `README.md` | This file |

---

## How to Run (Google Colab)

### Manual upload to Colab

1. Go to [colab.research.google.com](https://colab.research.google.com)
2. Click **File → Upload notebook**
3. Upload `AURN_Imputation_Pipeline.ipynb`
4. Upload `Greater_London.csv` to the Colab session files (click the folder icon on the left sidebar → upload)
5. Run all cells from top to bottom (**Runtime → Run all**)

---

## Dataset

The dataset `Greater_London.csv` is included in this repository. It contains hourly pollutant measurements from a Greater London AURN monitoring station across the full year 2024, obtained from the UK Air Quality Data Portal.

**Source:** [https://www.get-air-pollution-data.service.gov.uk](https://www.get-air-pollution-data.service.gov.uk)

**Pollutants included:** NO₂, O₃, PM10, PM2.5, SO₂

The raw dataset contains 8,784 hourly observations. After removing rows with pre-existing missing values, the clean ground-truth dataset used in this study contains **7,315 observations**.

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
- Five positive R² values were recorded: ozone under GAIN (0.341) and Random Forest (0.226), PM10 under GAIN (0.231), PM2.5 under Random Forest (0.303) and GAIN (0.068)
- Sulphur dioxide proved uniformly resistant across all methods due to weak inter-pollutant correlations

---

## Ethical Approval

This research relies exclusively on publicly available AURN records published by DEFRA. The data contains no personally identifiable information. Ethical approval was granted by the University of Sheffield Research Ethics Committee.

---

## Licence

This project is submitted as academic coursework at the University of Sheffield. All code is original unless otherwise cited in the dissertation.
