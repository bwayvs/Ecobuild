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

The dataset is based on computer simulations rather than measurements from
