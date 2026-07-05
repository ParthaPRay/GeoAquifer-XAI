# Explainable GeoAI-Based Mapping of Groundwater Contamination Hotspots and Aquifer-Linked BIS Exceedance Risk Across India

## Overview

Groundwater contamination in India varies across regions, aquifer systems, contaminant types, and hydrogeological settings. This project develops a national-scale geospatial artificial intelligence workflow to assess groundwater contamination hotspots and BIS exceedance risk.

The framework focuses on five major groundwater-quality indicators:

* Nitrate
* Fluoride
* Uranium
* Arsenic
* Electrical Conductivity / Salinity

The workflow standardizes contamination records, applies contaminant-specific BIS thresholds, maps spatial patterns, overlays contamination points with principal aquifer systems, predicts BIS exceedance risk using machine learning, explains model behaviour using SHAP, and performs spatial clustering of contamination points.

---

## Dataset

The input dataset file `Contamination_Hotspots.xlsx` used in this repository is based on the curated Kaggle dataset [Annual Ground Water Quality Report 2025 India](https://www.kaggle.com/datasets/mynkpandey/annual-ground-water-quality-report-2025-india). This curated dataset was prepared from official groundwater-quality source reports published by the Department of Water Resources, RD & GR, Ministry of Jal Shakti and the Central Ground Water Board (CGWB). The original source documents are available here: [Ministry of Jal Shakti report](https://www.jalshakti-dowr.gov.in/static/uploads/2025/11/2d2afc1bcaa06de10de2f1ffe3276780.pdf) and [CGWB report](https://cgwb.gov.in/cgwbpnm/public/uploads/documents/176302296020936587file.pdf).

---

## Key Features

### Groundwater Data Processing

The script reads and standardizes multi-sheet groundwater contamination data containing identified hotspot centres and surrounding grid samples. It harmonizes contaminant names, sample types, units, coordinates, BIS thresholds, exceedance status, exceedance ratios, and risk classes.

### BIS Exceedance Mapping

For each contaminant, the workflow evaluates whether groundwater samples exceed the corresponding BIS threshold. It generates log-transformed concentration and exceedance-ratio variables for more stable spatial visualization.

### Aquifer-System Integration

The workflow integrates the NWIC principal aquifer-system GeoJSON layer and corrects its coordinate reference system for India-scale analysis. Contamination points are spatially joined with aquifer polygons to support aquifer-linked contamination interpretation.

### Machine Learning

A leakage-safe binary classification pipeline is developed to predict BIS exceedance. The model uses geospatial, administrative, contaminant, sample-type, and aquifer-related predictors while excluding direct leakage variables such as raw concentration, exceedance ratio, and BIS threshold-derived target variables.

Models evaluated include:

* Logistic Regression
* Random Forest
* Extra Trees
* HistGradientBoosting
* XGBoost
* Neural network models
* Soft-voting hybrid models
* Stacking hybrid models

### Explainable AI

The final machine learning model is interpreted using SHAP-based explainable AI. Outputs include global feature importance, beeswarm plots, dependence plots, grouped feature importance, and local prediction explanations.

### Spatial Clustering

DBSCAN clustering is used to identify spatially concentrated contamination groups. Clustering is performed both overall and contaminant-wise.

---

## Repository Structure

```text
GeoAquifer-XAI/
│
├── geoaquifer_xai.py
├── README.md
└── outputs/
    ├── figures/
    ├── processed_data/
    ├── machine_learning/
    ├── probability_maps/
    ├── prediction_error_maps/
    ├── aquifer_overlay_contaminant_maps/
    └── contaminant_wise_cluster_maps/
```

The `outputs/` folders are generated automatically when the script is executed.

---

## Main Outputs

The workflow generates:

* Cleaned groundwater contamination dataset
* Aquifer-joined contamination dataset
* ML-ready dataset
* State-wise contamination summary
* District-wise contamination summary
* Aquifer-wise contamination summary
* Final ML prediction table
* GeoJSON prediction outputs
* Contaminant-wise maps
* Aquifer-overlay maps
* ML-predicted BIS exceedance probability maps
* Correct/incorrect prediction maps
* DBSCAN spatial cluster maps
* SHAP explanation plots
* ROC curve, precision-recall curve, and confusion matrix
* Final trained model file

---

## Requirements

The code is intended to run in Google Colab or a compatible Python environment.

Main dependencies include:

```text
geopandas
shapely
pyproj
rtree
mapclassify
contextily
folium
branca
openpyxl
matplotlib
matplotlib-scalebar
pandas
numpy
scikit-learn
xgboost
shap
joblib
```

---

## How to Run

Clone the repository:

```bash
git clone https://github.com/ParthaPRay/GeoAquifer-XAI.git
cd GeoAquifer-XAI
```

Run the Python script:

```bash
python geoaquifer_xai.py
```

For Google Colab, upload `geoaquifer_xai.py`, open it as a notebook-style script, and run the cells sequentially.

---

## Note on Notebook Version

The original Google Colab notebook exceeded GitHub’s direct upload limit. Therefore, the complete workflow has been uploaded as:

```text
geoaquifer_xai.py
```

Users may convert it back to a notebook using Jupyter or Jupytext if required.

Example:

```bash
pip install jupytext
jupytext --to notebook geoaquifer_xai.py
```

This will create:

```text
geoaquifer_xai.ipynb
```

---

## Suggested Citation

```text
Ray, P. P. (2026). GeoAquifer-XAI: Explainable GeoAI-Based Mapping of Groundwater Contamination Hotspots and Aquifer-Linked BIS Exceedance Risk Across India. GitHub repository. https://github.com/ParthaPRay/GeoAquifer-XAI
```

---

## Author

**Partha Pratim Ray**
Department of Computer Applications
Sikkim University, India

GitHub: [https://github.com/ParthaPRay](https://github.com/ParthaPRay)

---

## Disclaimer

This repository provides a research-oriented GeoAI workflow for groundwater contamination analysis. The outputs should not be treated as regulatory groundwater-quality decisions without validation by official agencies, hydrogeologists, and field-based water-quality assessment.

---

## Keywords

```text
GeoAI
Groundwater contamination
Aquifer mapping
BIS exceedance
Explainable AI
SHAP
India groundwater quality
Spatial clustering
DBSCAN
Geospatial machine learning
Environmental informatics
Hydrogeology
```

````

You may also add this short note at the top of the GitHub repository description:

```text
Explainable GeoAI workflow for groundwater contamination hotspot mapping, aquifer-linked BIS exceedance prediction, SHAP interpretation, and DBSCAN spatial clustering across India.
````
