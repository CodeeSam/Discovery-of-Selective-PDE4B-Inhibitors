# Computational Design of Novel Selective PDE4B Inhibitors from Natural Compounds

## Overview

This repository contains the complete machine learning pipeline for the manuscript:

> **"Computational Design of Novel Selective Phosphodiesterase 4B Inhibitors from Natural Products: An Integrated Machine Learning and Structure-Based Drug Discovery Approach"**

The pipeline integrates ligand-based ML screening with SHAP interpretability to prioritize PDE4B-active natural product candidates from the LOTUS database for downstream structure-based drug design.

---

## Repository Structure

```
PDE4B-Inhibitor-Discovery/
│
├── data/                          # Input data (not tracked by git — see below)
│   ├── PDE4B_Data.csv             # ChEMBL PDE4B bioactivity data
│   └── LOTUS_DB.smi               # LOTUS natural product SMILES
│
├── outputs/                       # Generated outputs (predictions, figures)
│   └── ...
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

---

## Data Requirements

The `data/` folder is not tracked by git due to file size. Before running the notebook, download the following files and place them in the `data/` directory:

### 1. PDE4B Bioactivity Data (`PDE4B_Data.csv`)
- Source: [ChEMBL Database](https://www.ebi.ac.uk/chembl/target/CHEMBL275)
- Target: Phosphodiesterase 4B (CHEMBL275)
- Filter: IC50 activity data only
- Download format: CSV
- Required columns: `Molecule ChEMBL ID`, `Smiles`, `pChEMBL Value`

### 2. LOTUS Natural Product Database (`LOTUS_DB.smi`)
- Source: [LOTUS Database](https://lotus.naturalproducts.net/download)
- Download: SMILES file (.smi format)
- Version used in this study: 276,518 compounds (accessed [DATE])

---

## Installation

### Option A — pip (recommended for quick setup)

```bash
git clone https://github.com/[your-username]/PDE4B-Inhibitor-Discovery.git
cd PDE4B-Inhibitor-Discovery
pip install -r requirements.txt
```

### Option B — Conda environment

```bash
git clone https://github.com/[your-username]/PDE4B-Inhibitor-Discovery.git
cd PDE4B-Inhibitor-Discovery
conda env create -f environment.yml
conda activate pde4b-env
```

---

## Running the Notebook

1. Clone the repository
2. Install dependencies (see above)
3. Download data files into `data/` (see Data Requirements)
4. Launch Jupyter:

```bash
jupyter notebook PDE4B_ML_Pipeline.ipynb
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

---

## Key Results

| Metric | Value |
|--------|-------|
| Best model | Random Forest |
| AUC-ROC (test set) | 0.955 |
| Accuracy (test set) | 0.891 |
| MCC (test set) | 0.784 |
| F1-Score (test set) | 0.891 |
| LOTUS compounds screened | 276,518 |
| Predicted strong inhibitors | 119,698 |
| After drug-likeness filtering | 14,210 |
| Top lead compound | LTS0048837 |

---

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

## Citation

If you use this code, please cite:

```
Computational Design of Novel Selective Phosphodiesterase 4B Inhibitors from Natural Products: An Integrated Machine Learning and Structure-Based Drug Discovery Approach
Samson Ayorinde Oni, Moyege Daniel Oyemomi, Osho Adebowale, Abdulfatai Abdulmalik
bioRxiv 2026.05.16.725619; doi: https://doi.org/10.64898/2026.05.16.725619
```

---

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.

---

## Contact

Corresponding author: [corresponding.author@institution.edu]
