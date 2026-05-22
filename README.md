# CrimeScope USA
### Big Data Crime Analysis: FBI National Incident-Based Reporting System (NIBRS)

> **ALY 6110: Big Data Analysis | Northeastern University**  
> Group project: Neeti Shah, Sukrit Tripathi, Edison, Khue Dinh

---
## Project Description
CrimeScope USA is an end-to-end big data pipeline and interactive Streamlit dashboard built on the FBI's **National Incident-Based Reporting System (NIBRS)** the most granular official U.S. crime dataset available. It spans **5.4M+ offense records** across **4 states and 4 years**, covering incident-level, victim-level, and offender-level data.

The project covers the full data science workflow: multi-table relational joins across 16 state-year folders, exploratory analysis of crime patterns by offense type, time, location, and demographics, machine learning classification models, time-series forecasting, and a prescriptive patrol allocation engine  all surfaced through a single interactive dashboard.

---
## Data Source
**FBI Uniform Crime Reporting (UCR) Program: NIBRS**  
Downloaded via the [Crime Data Explorer](https://cde.fbi.gov/dataexplorer)

## Team Contributions

### Neeti: `nibrs_crime_classification.ipynb`
Machine learning classification pipeline predicting whether a crime incident falls under **Person, Property, or Society** offenses. Covers multi-table join architecture, full sklearn Pipeline with ColumnTransformer preprocessing (OneHotEncoder + imputation), and comparison of four classifiers: Logistic Regression, Ridge Classifier, Decision Tree, and Random Forest — trained on 250,000 sampled records with 80/20 stratified split.

### Sukrit Tripathi: EDA + crime type classification
Core data ingestion architecture used by the entire team. Dynamic multi-folder loading across all 16 state-year directories. Full EDA on crime trends, offense distributions, and demographic breakdowns. Classification models predicting offense category and crime_against type.

### Edison: `Bigdata_EdisonContribution.ipynb`
Extended EDA with victim vs. offender demographic comparisons, weapon analysis, and geographic patterns. Binary arrest prediction models (Logistic Regression, Random Forest, Gradient Boosting) with ROC-AUC evaluation and ROC curves.

### Khue Dinh: `KHUE_DINH_BIG_DATA.ipynb`
Victim demographic deep-dive by age, race, ethnicity, and sex across states. Time-series forecasting of monthly crime volume using Ridge regression with lag features. Prescriptive patrol allocation model using linear programming (SciPy) with efficiency vs. fairness policy comparison.

---

## The Combined Dashboard (`big_data_group_project.py`)

A **Streamlit** app that brings all four contributions into one interactive interface. Run it locally with:

```bash
streamlit run big_data_group_project.py
```

**Dashboard sections:**
- **EDA** — crime trends by state/year, offense category breakdown, location heatmaps, crime_against trends over time
- **Victim Analysis** — age groups, race, ethnicity, sex breakdowns; victim vs. offender race comparison
- **Models (Sukrit)** — offense category and crime_against classification, combining the projects
- **Models (Edison)** — arrest likelihood prediction with ROC curves
- **Models (Neeti)** — crime_against classification pipeline with confusion matrices
- **Models (Khue)** — monthly crime forecasting + prescriptive patrol allocation

All sections respond to a **global sidebar filter** (state, year, offense category) so every chart and model updates together.

## Key Technical Highlights

- **Multi-table relational joins** across 11 NIBRS CSV tables per state-year folder, with careful bridge-table handling to avoid many-to-many row explosions
- **16 state-year folders** loaded dynamically — adding new states/years requires no code changes
- **sklearn Pipelines with ColumnTransformer** — imputation, one-hot encoding, and scaling all fitted on training data only, preventing data leakage
- **Streamlit caching** (`@st.cache_data`) keeps the dashboard fast even on 5M+ row datasets
- **Time-series forecasting** with lag features and rolling means using Ridge regression
- **Prescriptive analytics** via linear programming for patrol resource allocation under two policy objectives

---

## Acknowledgements
**Data:** FBI Uniform Crime Reporting Program — National Incident-Based Reporting System (NIBRS)  
**Course:** ALY 6110 — Big Data Analysis, Northeastern University  
**Original repository:** https://github.com/sukritt87/ALY_6110 (Revised as my project was not updated during the course of the class project)
