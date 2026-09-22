# Cardiovascular disease classification analysis

Research materials comparing Gradient Boosting, XGBoost, CatBoost and Extra Trees, with no balancing, class weighting and SMOTENC, on two public datasets.

## Status

This is a draft research archive. The notebook is preserved as an executed working record, including historical retries and export errors. It has not been verified to run top to bottom in a fresh runtime. Resolve cell order, remove obsolete retries, pin dependencies and verify a clean run before the final publication release. The manuscript must be updated to match these results.

## Data sources

- HDC: Maghdid, S. S., and Rashid, T. A. (2022), *An Extensive Dataset for the Heart Disease Classification System*, version 2. https://doi.org/10.17632/65gxgy2nmg.2 . Repository: https://data.mendeley.com/datasets/65gxgy2nmg/2 . The supplied Medicaldataset.arff was previously checked against the analysis CSV for matching values and record order.
- Cleveland: UCI Heart Disease repository, https://archive.ics.uci.edu/dataset/45/heart+disease . Use processed.cleveland.data, containing 303 records.

Raw datasets are obtained from their original repositories. Preserve original attribution and applicable dataset licences. The notebook expects the HDC CSV named `Heart Attack.csv` and the Cleveland file named `processed.cleveland.data`. HDC columns: age, gender, impluse, pressurehight, pressurelow, glucose, kcm, troponin, class. Labels are negative/positive. Cleveland has no header and uses ? for missing values; num > 0 is mapped to class 1.

## Contents

- analysis_working_record.ipynb: original executed Colab notebook, unchanged.
- cv_checkpoint/: split assignments, quality flags, baseline CV scores and recorded environment metadata.
- tuning_results/: tuning comparisons, test predictions, confidence intervals, SHAP, permutation importance and exploratory sensitivity analyses.
- tuning_results/HDC_lime_fidelity.csv and HDC_lime_coefficients.csv: recovered LIME exports, added to this package.

The previous archive's export_status.json was omitted because it predates recovery of the LIME files. The serialized model bundle is not included. Retained metadata files describe the original analysis checkpoint and may mention those original archive contents.

## Main results

Models were selected by training cross-validation ROC-AUC; test evaluation used threshold 0.50.

| Dataset | Selected pipeline | Test n | ROC-AUC | Accuracy | Recall |
|---|---|---:|---:|---:|---:|
| HDC | XGBoost + SMOTENC | 264 | 0.9838 | 0.9811 | 0.9815 |
| Cleveland | Extra Trees + class weighting | 61 | 0.9556 | 0.8852 | 0.9286 |

The HDC LIME explanation has limited fidelity: model probability 0.9988, local approximation 0.6768, weighted R-squared 0.4204. It must not be presented as an accurate reconstruction. Sensitivity analyses are exploratory training-only analyses performed after the main test evaluation. These materials support research on recorded dataset labels, not prospective clinical deployment.

## Reproduction and release checklist

1. Obtain the source datasets and prepare the exact input names and formats above.
2. Review the recorded package versions in the checkpoint metadata and notebook outputs.
3. Clean the working notebook's retries and order; execute in a fresh Colab runtime and compare outputs.
4. Select an appropriate licence for the original code; do not apply it to third-party datasets.
5. Publish a versioned release and archive it with a persistent identifier, then update the manuscript's availability statement.
