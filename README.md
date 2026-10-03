# Predicting Aqueous Solubility of Drug-like Molecules with Machine Learning

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Sparshith-2001/drug-solubility-prediction/blob/main/drug_solubility_prediction.ipynb)

## Overview
Poor aqueous solubility is one of the main reasons drug candidates fail during development. This project uses machine learning to predict the solubility (log S) of drug-like molecules from simple molecular descriptors, and compares a linear baseline with a random forest model.

## Dataset
- **ESOL (Delaney) dataset:** 1,128 organic molecules with experimentally measured aqueous solubility (log S, mol/L)
- **Features used:** molecular weight, polar surface area, number of rings, rotatable bonds, H-bond donors, minimum degree
- **Target:** measured log solubility
- The dataset's "ESOL predicted" column was deliberately excluded, as it contains another model's predictions and would leak information.

## Methods
1. **Exploratory data analysis:** distributions, correlation heatmap, scatter plots of each feature against log S
2. **Train/test split:** 80% training, 20% test (`random_state=42` for reproducibility)
3. **Models:** linear regression (baseline) and random forest regressor (300 trees)
4. **Evaluation:** R², RMSE and MAE on the held-out test set
5. **Interpretation:** model coefficients and random forest feature importance

## Results

| Model | R² | RMSE | MAE |
|---|---|---|---|
| Linear Regression | 0.696 | 1.199 | 0.892 |
| **Random Forest** | **0.826** | **0.908** | **0.604** |

The random forest reduced mean absolute error by about 32% compared with the linear baseline.

## Key findings
- **Molecular weight** was the strongest predictor of solubility (r = −0.64): larger molecules are less soluble.
- **Polar surface area** was the second most important feature in the random forest, despite a weak linear correlation (r = 0.12). This suggests its effect depends on molecular size, a non-linear interaction that linear regression cannot capture.
- The random forest greatly improved predictions for **very insoluble compounds** (log S below −7), which linear regression overestimated.
- Number of rings was correlated with solubility (r = −0.51) but had low importance in the random forest, as its information overlaps with molecular weight (r = 0.65).

## Limitations and future work
- Only six simple descriptors were used. Adding **logP** and other descriptors calculated with **RDKit** from the SMILES strings should improve accuracy.
- A few highly soluble compounds were underpredicted by both models.
- Results come from a single train/test split; **cross-validation** would give a more robust estimate.
- **Permutation importance** would give a more reliable feature ranking than impurity-based importance.

## Tools
Python, pandas, NumPy, scikit-learn, Matplotlib, seaborn, Google Colab

## Reference
Delaney, J. S. (2004). ESOL: Estimating Aqueous Solubility Directly from Molecular Structure. *Journal of Chemical Information and Computer Sciences*, 44(3), 1000–1005.

## Author
**Sparshith Victorbalu Sagayamary**
MSc Pharmaceutical Analysis, Queen's University Belfast
