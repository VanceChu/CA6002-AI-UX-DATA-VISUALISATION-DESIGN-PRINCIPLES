# Repository Guidelines

## Project Structure & Module Organization
The root contains course PDFs and the `Assignment/` workspace. Most code lives under:
- `Assignment/lightgbm_pipeline/`: the Home Credit LightGBM pipeline with `notebooks/`, `scripts/`, `models/`, `outputs/`, and the dataset folder `home-credit-default-risk/`.
- `Assignment/choice/`: EDA work for credit and ecommerce datasets, including `credit/` (Python + notebook + `eda_output/`) and `ecommerce/` (Python + notebook + PNG outputs).
- `Assignment/Home credit/`: a single exploratory notebook.

## Build, Test, and Development Commands
There is no build system; use Python and Jupyter directly.
- `jupyter lab` (or `jupyter notebook`) to run notebooks such as `Assignment/lightgbm_pipeline/notebooks/lightgbm_pipeline_notebook.ipynb`.
- `python Assignment/lightgbm_pipeline/scripts/lightgbm_with_simple_features.py` for the script-based pipeline (requires data in `home-credit-default-risk/`).
- `python Assignment/choice/credit/credit_eda_analysis.py` and `python Assignment/choice/ecommerce/ecommerce_eda_visualization.py` for EDA scripts.
In the main LightGBM notebook, set `TRAIN_MODE` and `DEBUG` in the first cell to control training vs. inference.

## Coding Style & Naming Conventions
Use Python/Notebook conventions: 4-space indentation, `snake_case` for functions/variables, and `CapWords` for classes. Keep paths relative to `Assignment/` and prefer saving generated artifacts under `outputs/` or `eda_output/`. No formatter or linter is configured, so keep cells short and readable.

## Testing Guidelines
No automated tests are present. Validate changes by re-running the impacted notebooks or scripts and checking generated outputs (plots, metrics, CSVs). If you add tests, use pytest conventions (`tests/`, `test_*.py`).

## Commit & Pull Request Guidelines
Commit history follows Conventional Commits with optional scopes, e.g., `feat(lightgbm): ...` or `refactor(lightgbm): ...`. PRs should include a concise summary, data sources used, runtime notes, and representative outputs (plots/metrics). Avoid committing large datasets or generated artifacts; `.gitignore` already excludes common data and model patterns.

## Data, Assets, and Outputs
Place Kaggle Home Credit CSVs under `Assignment/lightgbm_pipeline/home-credit-default-risk/`. Large datasets and models are ignored (e.g., `**/application_train.csv`, `**/ecommerce_customer_behavior_dataset*.csv`, `**/models/*.txt`), so keep committed outputs small and intentionally shareable.
