# EcoBuild — Research Notebook (Veronica Broadway)

**Project:** EcoBuild: Building Energy Efficiency Predictor  
**Researcher:** Veronica Broadway  
**Notebook:** `notebooks/EcoBuild_Research.ipynb`  
**Part of:** University of North Texas, DTSC 5082 research project

## Overview

This notebook examines how building design characteristics relate to simulated heating and cooling requirements. It looks beyond overall model accuracy by comparing different ways of testing predictions and checking whether errors differ between shorter and taller building configurations.

## Interactive Research Dashboard

The research findings are also presented in the **EcoBuild Energy Intelligence Research Story**, a standalone interactive HTML dashboard.

**[Open the Live EcoBuild Research Dashboard](https://bwayvs.github.io/Ecobuild/notebooks/EcoBuild_Energy_Intelligence_Research_Story.html#eda)**

The dashboard includes seven views covering data exploration, key findings, model performance, validation methods, model reliability, design characteristics, and data governance.

It allows readers to explore heating and cooling results, compare prediction errors, and review the limitations of the simulated dataset.

The dashboard is a research communication tool, separate from the team's Streamlit application. It has not been formally evaluated through user testing.

My focus is **data quality, exploratory analysis, model reliability, and responsible interpretation of the results**. This notebook supports my individual research paper and the EcoBuild decision-support dashboard. It is not the team's production application.

## Dataset

The notebook uses the public **UCI Energy Efficiency dataset (ID 242)**, originally described by Tsanas and Xifara (2012).

- **768 records** with **8 building inputs** (`X1`–`X8`) and **2 simulated outcomes**: heating load (`Y1`) and cooling load (`Y2`).
- Inputs describe relative compactness, surface area, wall area, roof area, height, orientation, glazing area, and glazing distribution.
- There are **192 distinct designs when orientation is excluded**, with each design evaluated at four orientations.
- These are **simulation results, not measurements from actual occupied buildings**.

Dataset: https://archive.ics.uci.edu/dataset/242/energy+efficiency  
Original paper: https://doi.org/10.1016/j.enbuild.2012.03.003

## What the notebook does

1. Checks dataset structure, missing values, and feature distributions.
2. Explores heating and cooling loads across building characteristics, including height.
3. Splits the data into **80% training / 20% testing** (`random_state=42`; 614/154 records).
4. Compares a mean baseline, Linear Regression, Random Forest, and Gradient Boosting using five-fold cross-validation on the training portion and evaluation on the holdout portion.
5. Reports **MAE**, **RMSE**, and **R²** for heating and cooling predictions.
6. Examines errors separately for **3.5 m** and **7.0 m** building configurations.
7. Compares ordinary random-row testing with whole-design testing, including **20 repeated splits** by default.
8. Reviews model feature importance and creates tables, figures, and research-ready exports.

The notebook also includes a separate, more restrictive geometry-only validation check. These tests answer different questions and should not be treated as interchangeable.

## How to run

### Option A — Google Colab (recommended)

1. Open [Google Colab](https://colab.research.google.com/).
2. Choose **Upload** and select `notebooks/EcoBuild_Research.ipynb` from this repository.
3. Select **Runtime → Run all**.
4. Allow the initial cell to install `ucimlrepo` if prompted. The notebook automatically attempts to download the public UCI dataset.
5. Review the results and download `EcoBuild_Research_Results.zip` when execution finishes.

**Internet access is needed** for the automatic UCI dataset download and, if needed, package installation. If the dataset cannot be downloaded, upload an authentic ENB2012 dataset file to the notebook's working directory and rerun the dataset-loading cell. Supported fallback names are `EcoBuild Data - ENB2012_data.xlsx`, `ENB2012_data.xlsx`, or `ENB2012_data.csv`. The notebook does **not** create substitute data.

### Option B — Run locally

Use Python 3 with Jupyter Notebook or JupyterLab. Install the dependencies:

```bash
python -m pip install jupyter numpy pandas matplotlib scikit-learn ucimlrepo openpyxl ipython
jupyter notebook notebooks/EcoBuild_Research.ipynb
```

Then choose **Run All Cells** in Jupyter. `openpyxl` is needed only when loading an Excel fallback dataset.

## Outputs

Running the notebook creates:

- `ecobuild_research_outputs/` — CSV tables, figures, and `methods_metadata.json` with the run settings and software versions.
- `EcoBuild_Research_Results.zip` — an archive of those generated files.

Useful tables include:

| File | Contents |
|---|---|
| `table_01_data_quality.csv` | Variable-level data checks |
| `table_04_training_cross_validation.csv` | Model comparison on training folds |
| `table_05_final_holdout_models.csv` | Final test-set model results |
| `table_07_height_group_reliability.csv` | Errors for shorter vs. taller configurations |
| `table_08_height_disparity_summary.csv` | Height-group error differences and ratios |
| `table_11_row_vs_design_fixed_holdouts.csv` | Fixed random-row vs. whole-design comparison |
| `table_12_repeated_split_raw.csv` | Results for each repeated split |
| `table_13_repeated_split_summary.csv` | Summary across repeated splits |
| `table_14_grouped_holdout_height_audit.csv` | Height errors on the whole-design holdout |
| `table_15_grouped_holdout_height_disparity.csv` | Grouped-holdout height disparity summary |

The notebook contains additional plots, tables, and explanatory notes. It uses `REPEATS = 20` for the repeated-split study; changing this value changes the number of runs and potentially the reported summaries.

## Team contributions and scope

EcoBuild is a team project. **Namita Moses** led the team's machine-learning development, grouped-validation work, and SHAP analysis. **Anthony Chavez** developed the product marketing and go-to-market research. This notebook documents my individual analysis and includes clearly identified references to the team's methods; it does not reproduce the full team application or claim ownership of teammates' work.

Team repository: https://github.com/njoanna12/ecobuild-app

## Important limitations

- Results are measured against **simulated heating and cooling loads**, not real-world electricity bills or observed energy use.
- Higher error for one building-height group is not, by itself, evidence that height causes poorer predictions; other building characteristics differ between groups.
- Comparisons based on absolute errors can reflect differences in the size of heating and cooling loads.
- The repeated splits overlap; their variation is **descriptive**, not a formal statistical confidence interval.
- The notebook does not establish real-building performance, actual savings, or the effectiveness of the dashboard through user testing.

## Citation

Tsanas, A., and Xifara, A. (2012). *Accurate quantitative estimation of energy performance of residential buildings using statistical machine learning tools*. Energy and Buildings, 49, 560–567. https://doi.org/10.1016/j.enbuild.2012.03.003
