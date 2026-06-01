# Computational Design of Novel Selective PDE4B Inhibitors from Natural Compounds

## Overview

This repository contains the complete machine learning pipeline for the manuscript:

> **"Integrated Machine Learning and Structure-Based Prioritization of Natural Product-Derived PDE4B-Selective Inhibitor Candidates"**

The pipeline integrates ligand-based ML screening with SHAP interpretability to prioritize PDE4B-active natural product candidates from the LOTUS database for downstream structure-based drug design.

---

## Repository Structure

```
Discovery-of-Selective-PDE4B-Inhibitors/
│
├── data/                          # Input data (not tracked by git — see below)
│   ├── PDE4B_Data.csv             # ChEMBL PDE4B bioactivity data
│   └── LOTUS_DB.smi               # LOTUS natural product SMILES
│
│
├── models/                        # Saved trained model
│   └── best_pde4_model_with_features.pkl
│
├── PDE4B_ML_Pipeline.ipynb        # Main analysis notebook
├── requirements.txt               # Python dependencies
├── environment.yml                # Conda environment (alternative)
├── .gitignore
└── README.md
```

## Installation

### Option A — pip (recommended for quick setup)

```bash
git clone https://github.com/CodeeSam/Discovery-of-Selective-PDE4B-Inhibitors.git
cd Discovery-of-Selective-PDE4B-Inhibitors
pip install -r requirements.txt
```

### Option B — Conda environment

```bash
git clone https://github.com/CodeeSam/Discovery-of-Selective-PDE4B-Inhibitors.git
cd Discovery-of-Selective-PDE4B-Inhibitors
conda env create -f environment.yml
conda activate pde4b-env
```

---

## Running the Notebook

1. Clone the repository
2. Install dependencies (see above)
3. Launch Jupyter:

```bash
jupyter notebook PDE4B_ML_Pipeline_Reproducible.ipynb
```

5. Run all cells in order. The first cell will create the required `data/`, `outputs/`, and `models/` directories automatically.

---

## Pipeline Summary

| Step | Description | Output |
|------|-------------|--------|
| 1 | ChEMBL PDE4B data curation | Cleaned bioactivity dataset |
| 2 | Descriptor calculation (217 RDKit 2D descriptors) | Descriptor matrix |
| 3 | Feature selection (variance → correlation → SelectKBest) | 20 features |
| 4 | Model training (5 classifiers, GridSearchCV, StratifiedKFold) | Best model: Random Forest |
| 5 | SHAP interpretability analysis | Feature importance plots |
| 6 | LOTUS database screening (276,518 compounds) | 119,698 predicted actives |
| 7 | Lipinski + PAINS + QED filtering | 14,210 drug-like candidates |
| 8 | Applicability domain (PCA) | Chemical space overlap plot |

Structure-based drug design steps (molecular docking, MM-GBSA, MD simulation) were performed using Schrödinger Maestro and are not reproduced in this notebook.

## Dependencies

See `requirements.txt` for the full list. Key packages:

- `rdkit` — molecular descriptor calculation and PAINS filtering
- `scikit-learn` — ML models, feature selection, cross-validation
- `xgboost`, `lightgbm` — gradient boosting classifiers
- `shap` — model interpretability
- `pandas`, `numpy` — data handling
- `matplotlib`, `seaborn` — visualization
- `joblib` — model serialization

---

```

---

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.

---
## Contact: ayosamoni@gmail.com
