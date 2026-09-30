# File-layout correction — 30 September 2026

Base commit: 1442ce965c3788a5e6fccea4cdcc65592e013ca2.

## Changes

- Both notebooks now resolve the actual MASTER_DATASET and MASTER_DATASET_EV input folders.
- New results stay under the repository root in model-specific timestamped directories.
- The setup fails with a clear message if the repository/input is missing.
- README and reproducibility instructions match the current folder layout.
- Notebook embedded outputs were cleared; frozen CSV/Excel/figure/model files remain unchanged.
- MANIFEST.sha256 was rebuilt for the complete distributed snapshot.

## Validation

Both notebooks compile. Path discovery and directory creation were exercised from the repository root, RF folder and XGB folder. Missing repository and missing input cases raise errors. All code outside path setup and the input-location error message is unchanged. Existing data, model parameters and frozen output files are byte-identical to the base commit.

Full training was not repeated; this is a path/documentation correction, not a new scientific analysis or a source-record audit.
