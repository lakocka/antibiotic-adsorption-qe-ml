# Reproducibility guide

## 1. Reference environment

The frozen model configurations record the following core environment:

- Python 3.13.9
- NumPy 2.3.5
- pandas 2.3.3
- scikit-learn 1.7.2
- SHAP 0.52.0
- Matplotlib 3.10.6
- XGBoost 3.3.0 (XGBoost notebook only)

The serialized `.joblib` files are version-sensitive. For reproducibility across environments, rerunning the notebooks from the supplied CSV inputs is preferred over loading a serialized estimator created under substantially different library versions.

## 2. Create an environment

Windows PowerShell example:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
```

## 3. Input data

Both notebooks discover the repository root from the current working directory or its parents. Keep the full extracted folder structure intact.

Repository inputs:

- `MASTER_DATASET/dataset.csv` — 213 modeling observations,
- `MASTER_DATASET_EV/dataset_EV.csv` — 19 external-validation observations.

Both files use semicolon delimiters and the standardized columns:

`MLOGP; C0_mg_L; pH; Temperature_C; Contact_time_min; Dose_g_L; BET_m2_g; qe_mg_g`

## 4. Run the notebooks

Run, in any order:

- `RF/RF_qe.ipynb`
- `XGB/XGB_qe.ipynb`

Each notebook uses a fixed random state and the predefined Training/Validation split.

The internal-validation procedure is **RepeatedKFold(n_splits=5, n_repeats=10, random_state=42)** and is performed only on the 143-record Training subset. The fixed 70-record Validation set and the 19-record External validation dataset are not used in internal CV.

## 5. Output location

The notebooks write new outputs to one folder inside the repository:

- `Adsorption_qe_ML_results/Random_Forest/<timestamp>/`
- `Adsorption_qe_ML_results/XGBoost/<timestamp>/`

Each run contains `Figures/`, `Tables/`, `Model/` and a consolidated Excel workbook. Timestamped run directories avoid overwriting previous outputs. The timestamp is generated when the setup cell runs; restart and run all cells to begin a new run.

Existing reference outputs remain in `RF/Adsorption_qe_ML_results/Random_Forest/` and `XGB/Adsorption_qe_ML_results/XGBoost/`.

## 6. Expected evaluation design

- Training: 143 observations
- Validation: 70 observations
- External validation: 19 observations
- Repeated 5-fold CV ×10: 50 internal validation-fold evaluations on Training only

CV R², MAE, and RMSE are reported as mean ± sample standard deviation across the 50 validation folds.

## 7. Integrity verification

`MANIFEST.sha256` contains SHA-256 checksums for all repository files except the manifest itself.

On systems with `sha256sum`:

```bash
sha256sum -c MANIFEST.sha256
```

On Windows, checksums can also be verified with `Get-FileHash` in PowerShell.

## Scope of the September 30 correction

Input discovery was tested from the root and both notebook folders. Model definitions, feature order, split, CV and export calculations remain unchanged. The complete training was not rerun for this file-layout-only correction. Notebook embedded outputs were cleared to avoid displaying stale paths; reference result files are preserved.
