# 🌱 Vegetation Cover Prediction in Tunisia under Climate Change Scenarios

This repository contains the code and resources developed during a research internship at the Laboratory of Ecology, Systematics, and Evolution (ESE) – Université Paris-Saclay.

## 🧠 Objective

The goal of this project is to predict the **future evolution of vegetation cover in Tunisia** under climate change (SSP245 scenario), using advanced **machine learning techniques** and large-scale **geospatial and bioclimatic data**.

---

## 📦 Key Data Sources and Preprocessing

### 🌍 Vegetation and Climate Data

- **Vegetation data** comes from **GLAD 2019 maps** (Global Land Analysis and Discovery Lab, University of Maryland), based on **Landsat imagery** with a **30m spatial resolution**. Each pixel is labeled with one of 20 land cover classes (0 to 19).  
  For this project, only the two tiles covering Tunisia (`40N_010E` and `40N_000E`) were used and processed via QGIS.

- **Climate data** (BIO1–BIO19) from [WorldClim](https://worldclim.org) was used for both the current period (1970–2000) and future projections (2021–2040) under **SSP245** scenario.

### 🗺️ Geographic Processing with QGIS

Using **QGIS**, we carried out the following:
- Extracted the **geographic boundary of Tunisia**.
- Generated a **1km² resolution pixel grid** over the country.
- Overlaid and fused the **vegetation maps** using zonal statistics ("majority" rule).
- Assigned the **dominant vegetation class** to each 1km² grid cell.
- Aligned 19 climatic variables (BIO1–BIO19) with each pixel.
- Produced two final datasets (Excel/CSV) with:
  - Coordinates (lat, lon)
  - Dominant vegetation class
  - 19 bioclimatic variables

These datasets served as the inputs for all machine learning models.

---

## 📊 Workflow Overview

### 1. **Data Processing**
- Removal of missing values.
- Dimensionality reduction via **correlation analysis**.
- **Standardization** of selected variables using z-score scaling.
- Aggregation of 20 original vegetation classes into 3 simplified categories.
- **Class balancing** via **random undersampling**.

### 2. **Modeling**
Implemented and evaluated several models:
- `Random Forest`
- `XGBoost`
- `SVM (Support Vector Machine)`
- Neural Network (exploratory only)

Each model was:
- Trained on current climate + vegetation data.
- Tested on a held-out sample.
- Applied to **future climate inputs** to predict vegetation changes in 2041–2060.

### 3. **Model Evaluation**
- Used metrics: **Accuracy, Precision, Recall, F1 Score, ROC-AUC**, and **True Skill Statistic (TSS)**.
- Best performance achieved by `Random Forest` and `XGBoost`.

## 🧠 Models Summary

| Model          | AUC Mean | Precision | Recall | F1 Score | TSS   |
|----------------|----------|-----------|--------|----------|-------|
| Random Forest  | 0.9366   | 0.7770    | 0.8946 | 0.8274   | 0.8693 |
| XGBoost        | 0.9333   | 0.7801    | 0.8854 | 0.8260   | 0.8554 |
| SVM            | 0.9800   | 0.7295    | 0.8669 | 0.7850   | 0.8374 |


## 🧾 Key Takeaways
- **Random Forest and XGBoost** are the most balanced and interpretable models.
- **BIO1 (mean temperature)** and **BIO12 (annual precipitation)** are the most impactful variables.
- Models predict a significant **decline in forest cover** in northern Tunisia under SSP245 scenario.


## 👤 Author

**Omar Maalej**  
🎓 ENSTA Paris – Data Science & Optimization  
📫 omar.maalej@ensta-paris.fr  
🔗 [LinkedIn](https://linkedin.com/in/omar-maalej-8a5615284)

---

## 📄 License

This repository and its contents are non-confidential and may be publicly shared for academic and research purposes
