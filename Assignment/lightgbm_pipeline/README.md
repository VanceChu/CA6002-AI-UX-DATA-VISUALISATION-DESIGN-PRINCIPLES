# LightGBM Pipeline for Home Credit Default Risk

[English](README.md) | [中文](README_CN.md)

This project implements a complete machine learning pipeline for the [Home Credit Default Risk](https://www.kaggle.com/c/home-credit-default-risk) Kaggle competition.

## Project Structure

```
lightgbm_pipeline/
├── README.md                 # This file
├── README_CN.md              # Chinese README
├── requirements.txt          # Python dependencies for notebooks/scripts
├── notebooks/
│   ├── lightgbm_pipeline_notebook.ipynb          # Main notebook (supports train/inference modes)
│   └── lightgbm_pipeline_notebook_executed.ipynb # Executed notebook with outputs
├── scripts/
│   └── lightgbm_with_simple_features.py          # Original Python script
├── models/                                       # Saved models (generated after training)
│   ├── lgbm_fold_0.txt ~ lgbm_fold_9.txt         # 10 fold models (LightGBM native format)
│   └── feature_list.pkl                          # Feature list for inference
├── outputs/                                      # Training/inference outputs
│   ├── exports/                                  # Exported artifacts (tables/plots)
│   ├── visualizations/                           # Charts and figures
│   ├── predictions/                              # Submission files
│   └── logs/                                     # Metrics and run logs
└── home-credit-default-risk/                     # Kaggle data (Git LFS)

**Note**: All output files (predictions, visualizations, logs) are automatically suffixed with a timestamp (e.g., `_20260117_232817`) to prevent overwriting.
```

## Environment Setup

Install dependencies:

```bash
python -m pip install -r requirements.txt
```

Launch notebooks with `jupyter lab` or `jupyter notebook`.

## Usage

### Configuration

In the first cell of `lightgbm_pipeline_notebook.ipynb`:

```python
TRAIN_MODE = True   # True: train new models, False: load saved models
DEBUG = False       # True: use 10000 rows for quick testing
```

### Training Mode (`TRAIN_MODE = True`)

1. Loads all data and performs feature engineering
2. Trains 10-fold LightGBM models
3. Saves models to `models/` directory
4. Generates visualizations and submission file
5. **Time**: ~30-40 minutes (full data)

### Inference Mode (`TRAIN_MODE = False`)

1. Loads all data and performs feature engineering
2. Loads pre-trained models from `models/` directory
3. **Performs OOF Evaluation**: Recreates validation splits to calculate AUC and OOF scores
4. **Generates Visualizations**: Creates ROC curves and feature importance plots
5. **Generates Predictions**: Creates submission file for test set
6. **Time**: ~5-10 minutes

## Results

| Metric | Value |
|--------|-------|
| 10-Fold Mean AUC | 0.7917 |
| OOF AUC | 0.7917 |
| Best Fold (Fold 5) | 0.7966 |
| Worst Fold (Fold 6) | 0.7852 |

## Data Requirements

The competition data lives in `./home-credit-default-risk/`. Large CSVs are tracked with Git LFS; after cloning, run `git lfs pull` if needed.

Files used by the pipeline:
- application_train.csv
- application_test.csv
- bureau.csv
- bureau_balance.csv
- previous_application.csv
- POS_CASH_balance.csv
- installments_payments.csv
- credit_card_balance.csv
- sample_submission.csv
- HomeCredit_columns_description.csv (reference)

## Dependencies

See `requirements.txt` for the full list (Python 3.8+). Key libraries include LightGBM, pandas, numpy, scikit-learn, matplotlib, seaborn, joblib, and SHAP.
