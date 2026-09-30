# Machine-learning prediction of antibiotic adsorption capacity

Experimental antibiotic adsorption capacity, qe (mg g⁻¹), modeled using Random Forest (RF) and XGBoost (XGB).

## Repository layout

- `MASTER_DATASET/dataset.csv`: numeric modeling input, 213 records.
- `MASTER_DATASET/213_records_final.xlsx`: detailed source dataset.
- `MASTER_DATASET_EV/dataset_EV.csv`: numeric external input, 19 records.
- `MASTER_DATASET_EV/19_records_external_validation_final.xlsx`: detailed external dataset.
- `RF/RF_qe.ipynb` and `XGB/XGB_qe.ipynb`: analysis notebooks.
- `RF/Adsorption_qe_ML_results/` and `XGB/Adsorption_qe_ML_results/`: existing reference outputs.
- `requirements.txt`: analysis dependencies.
- `REPRODUCIBILITY.md`: environment, execution and evaluation design.
- `MANIFEST.sha256`: checksums for the distributed snapshot.

## Run

Download and extract the full repository. Follow `REPRODUCIBILITY.md` to install dependencies, then start `jupyter lab` from the repository root. Open either notebook and run all cells in order. Both notebooks locate data from the root or nested working directories.

New outputs are written inside the repository, under `Adsorption_qe_ML_results/<model>/<timestamp>/`. Existing reference outputs are not overwritten. No Desktop path is required.

## Evaluation

The fixed split uses 143 Training and 70 Validation observations. Repeated 5-fold cross-validation ×10 is performed on Training only. The external dataset contains 19 observations. Model settings and numerical reference outputs were not changed by the 30 September 2026 path/documentation correction.

The correction verifies file organization and input discovery; it does not constitute a new source-paper audit or a new full model run. See `TECHNICAL_FIX_20260930.md`.
