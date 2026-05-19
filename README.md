# Dhemaji Flood Prediction

Machine learning-based flood prediction system for Dhemaji district, Assam, India using satellite-derived data on a 500m × 500m grid.

---

## Project Overview

This project develops a flood prediction model for Dhemaji district, one of the most flood-prone regions in India due to Brahmaputra river overflow during monsoon season. The model uses Sentinel-1 SAR for ground-truth flood labels and combines multiple satellite data sources to predict flooding at high spatial resolution.

---

## Final Model Performance

| Metric | Value |
|---|---|
| Precision | 0.85 |
| Recall | 0.82 |
| F1 Score | 0.83 |
| ROC-AUC | 0.990 |
| Best Threshold | 0.4 |

---

## Study Area

- **Location**: Dhemaji District, Assam, India
- **Bounding Box**: 27.40-27.75 N, 94.35-94.85 E
- **Grid Resolution**: 500m × 500m
- **Total Grid Cells**: ~8,658
- **Years Covered**: 2019-2024 monsoon seasons

---

## Data Sources

| Source | Type | Resolution | Platform |
|---|---|---|---|
| Sentinel-1 SAR | Flood Labels | 500m | Google Earth Engine |
| CHIRPS | Daily Rainfall | 5km | Google Earth Engine |
| ERA5 Land | Daily Runoff | 11km | Google Earth Engine |
| HydroSHEDS | River Network | Vector | Google Earth Engine |
| SRTM | Elevation/Slope | 30m | Google Earth Engine |
| MODIS | Tree Cover | 500m | Google Earth Engine |

---

## Methodology

1. **Flood Labels**: Sentinel-1 VV backscatter < -15 dB classified as water

2. **Features Engineered**
   - Spatial:
     - distance to major river
     - elevation
     - slope
     - tree cover
   - Temporal:
     - daily rainfall
     - 3/5-day cumulative rainfall
     - rainfall anomaly
   - Runoff:
     - ERA5 runoff sum
     - runoff anomaly

3. **Model**
   - Gradient Boosting Classifier
   - max_features = 3

4. **Validation**
   - Temporal split:
     - Train: 2019-2023
     - Test: 2024

---

## Repository Structure

```text
dhemaji-flood-prediction/
├── README.md
├── requirements.txt
├── notebooks/
│   ├── 01_data_collection_gee.ipynb
│   ├── 02_data_processing.ipynb
│   ├── 03_eda.ipynb
│   ├── 04_model_training.ipynb
│   ├── 05_final_model_evaluation.ipynb
│   └── 06_visualizations.ipynb
├── data/
│   ├── raw/
│   └── processed/
├── models/
├── results/
└── figures/
