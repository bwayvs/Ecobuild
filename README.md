# EcoBuild — Research Notebook (Veronica Broadway)

**Project:** EcoBuild: Building Energy Efficiency Predictor  
**Researcher:** Veronica Broadway  
**Notebook:** [EcoBuild_Research.ipynb](https://github.com/bwayvs/Ecobuild/blob/main/notebooks/EcoBuild_Research.ipynb)  
**Part of:** University of North Texas, DTSC 5082 research project

## Overview

This research examines how building design characteristics relate to simulated heating and cooling requirements. It looks beyond overall model accuracy by comparing different validation methods and examining whether prediction errors differ between shorter and taller building configurations.

My individual contributions focus on **data quality, exploratory data analysis, model comparison, prediction reliability, validation methods, and responsible interpretation of results**.

The research supports the EcoBuild project and its interactive decision-support dashboard. It is separate from the team's production application.

## Open the Research Notebook Online

**[Open the EcoBuild Research Notebook in Google Colab](https://colab.research.google.com/drive/1LH8qB-0MDEsiyinA4N855QZn0H-jk1iD)**

The Google Colab notebook allows readers to view the research online and, with appropriate access and a Colab runtime, execute the analysis without installing Python locally.

The notebook source is also available on GitHub:

[View EcoBuild_Research.ipynb on GitHub](https://github.com/bwayvs/Ecobuild/blob/main/notebooks/EcoBuild_Research.ipynb)

## Interactive Research Dashboard

The research findings are presented in the **EcoBuild Energy Intelligence Research Story**, a standalone interactive HTML dashboard.

**[Open the Live EcoBuild Research Dashboard](https://bwayvs.github.io/Ecobuild/notebooks/EcoBuild_Energy_Intelligence_Research_Story.html#eda)**

The dashboard contains seven research views:

1. **Explore the data:** Building characteristics, data distributions, and heating and cooling loads.
2. **What the evidence says:** Key research findings.
3. **How well do the models predict?** Model comparisons and performance metrics.
4. **Does validation change the answer?** Comparison of random-row and whole-design testing.
5. **Where is the model less reliable?** Prediction error comparisons between building-height groups.
6. **Which design features matter?** Building characteristics associated with model predictions.
7. **What can we responsibly conclude?** Data quality, governance, limitations, and responsible interpretation.

The dashboard allows readers to explore heating and cooling results, evaluate model reliability, and understand the limitations of the simulated dataset.

It is a research communication tool, not the team's Streamlit application. Its effectiveness has not been formally evaluated through user testing.

## Dataset

The research uses the publicly available **UCI Energy Efficiency dataset (ID 242)**, originally described by Tsanas and Xifara (2012).

The dataset contains:

- **768 simulated building configurations**
- **8 input variables** (`X1`–`X8`)
- **2 target variables:** Heating load (`Y1`) and cooling load (`Y2`)
- **192 distinct designs** when orientation is excluded, with each evaluated at four orientations

The building inputs describe relative compactness, surface area, wall area, roof area, overall height, orientation, glazing area, and glazing distribution.

The dataset is based on computer simulations rather than measurements from occupied buildings.

**Dataset:** https://archive.ics.uci.edu/dataset/242/energy+efficiency

**Original research:** https://doi.org/10.1016/j.enbuild.2012.03.003

## What the Research Notebook Does

The notebook documents the following analyses:

1. Reviews dataset structure, data types, missing values, and feature distributions.
2. Explores relationships between building characteristics and heating and cooling requirements.
3. Divides records into **80% training and 20% testing**, using `random_state=42`.
4. Compares a mean baseline, Linear Regression, Random Forest, and Gradient Boosting.
5. Uses five-fold cross-validation on the training data and evaluates performance on held-out records.
6. Reports Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), and R².
7. Evaluates prediction errors separately for **3.5-meter and 7.0-meter** building configurations.
8. Compares random-row and whole-design validation, including 20 repeated splits.
9. Examines model feature importance.
10. Generates research tables, charts, and supporting output files.

The notebook also includes a stricter geometry-only validation check. This is a separate sensitivity analysis and should not be interpreted as equivalent to whole-design validation.

## How to Reproduce the Research

### Option A — Google Colab (Recommended)

1. Open the [EcoBuild Research Notebook in Google Colab](https://colab.research.google.com/drive/1LH8qB-0MDEsiyinA4N855QZn0H-jk1iD).
2. Sign in with a Google account if prompted.
3. If the notebook is read-only, select **File → Save a copy in Drive** to create an editable copy.
4. Select **Runtime → Run all**.
5. Allow the notebook to install `ucimlrepo` if prompted.
6. The notebook will attempt to download the public UCI Energy Efficiency dataset.
7. Review the generated results and download `EcoBuild_Research_Results.zip` when execution finishes.

Internet access is required for downloading the dataset and installing dependencies.

If automatic dataset retrieval fails, an authentic ENB2012 dataset file can be uploaded to the notebook's working directory. Supported fallback filenames are:

- `EcoBuild Data - ENB2012_data.xlsx`
- `ENB2012_data.xlsx`
- `ENB2012_data.csv`

The notebook does not generate substitute data.

### Option B — Run Locally

Download or clone this repository and open a terminal in its root directory.

Install the dependencies:

```bash
python -m pip install jupyter numpy pandas matplotlib scikit-learn ucimlrepo openpyxl ipython
```

Open the notebook:

```bash
jupyter notebook notebooks/EcoBuild_Research.ipynb
```

Select **Run All Cells** in Jupyter.

The `openpyxl` package is needed when loading an Excel fallback dataset.

## Research Outputs

Running the notebook generates:

- `ecobuild_research_outputs/` — Research tables, figures, and methodology metadata.
- `EcoBuild_Research_Results.zip` — Archive of generated research outputs.
- `methods_metadata.json` — Run settings and software-version information.

Important output tables include:

| File | Description |
|---|---|
| `table_01_data_quality.csv` | Data-quality checks |
| `table_04_training_cross_validation.csv` | Training cross-validation results |
| `table_05_final_holdout_models.csv` | Final model performance |
| `table_07_height_group_reliability.csv` | Prediction errors by building height |
| `table_08_height_disparity_summary.csv` | Height-group error differences and ratios |
| `table_11_row_vs_design_fixed_holdouts.csv` | Fixed validation comparison |
| `table_12_repeated_split_raw.csv` | Results from individual repeated splits |
| `table_13_repeated_split_summary.csv` | Summary of repeated validation results |
| `table_14_grouped_holdout_height_audit.csv` | Height reliability under whole-design validation |
| `table_15_grouped_holdout_height_disparity.csv` | Whole-design subgroup error comparison |

The repeated-validation analysis uses `REPEATS = 20` by default. Changing this setting can change the resulting summaries.

## Main Research Findings

The research identified several important findings:

- Gradient Boosting achieved strong prediction accuracy for simulated heating and cooling loads.
- Holding out entire building designs increased average heating-load MAE by approximately **41.8%** compared with random-row testing across 20 repeated splits.
- Prediction errors differed between shorter and taller building configurations.
- Taller configurations showed larger absolute errors, but also had substantially greater heating and cooling requirements.
- Overall prediction accuracy alone did not fully describe how models performed across different validation methods or building groups.

These findings support evaluating prediction reliability and communicating model limitations rather than relying exclusively on a single overall accuracy score.

## Team Contributions and Individual Research Scope

EcoBuild was developed as a team project.

**Veronica Broadway:** Exploratory data analysis, data-quality review, independent model comparisons, repeated validation analysis, building-height reliability analysis, data governance, and development of the interactive research dashboard.

**Namita Moses:** Team machine-learning development, grouped validation, model tuning, and SHAP explainability analysis.

**Anthony Chavez:** Product marketing, intended-user research, market analysis, and go-to-market strategy.

This repository documents my individual research and dashboard. It does not reproduce the complete team application.

**Team repository:** https://github.com/njoanna12/ecobuild-app

**Team reproduction instructions:** https://github.com/njoanna12/ecobuild-app/blob/main/README.md

## Research Limitations

- The dataset contains simulated results, not actual electricity bills or measured building performance.
- Only a limited number of building designs and two overall-height values are represented.
- Prediction-error differences between height groups do not establish that height causes those differences.
- Larger absolute errors may partly reflect larger heating or cooling requirements.
- Repeated validation splits share observations. Their reported variation is descriptive rather than an independent-sample confidence interval.
- Results do not establish how accurately the models would predict actual buildings.
- The interactive dashboard has not been evaluated through formal user testing.
- The models are research tools and should not replace professional building-energy simulations or engineering evaluations.

## Citation

Tsanas, A., and Xifara, A. (2012). *Accurate quantitative estimation of energy performance of residential buildings using statistical machine learning tools*. Energy and Buildings, 49, 560–567.

https://doi.org/10.1016/j.enbuild.2012.03.003
