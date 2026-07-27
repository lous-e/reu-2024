# scripts/

R scripts for an NFL win-probability modeling pipeline. Run in numeric order.

### 0_get_pbp_data.R
Downloads a season of play-by-play data via `nflreadr` and saves it as CSV.

### 1_clean_data.R
Cleans a season's play-by-play data: filters to regular-season plays, buckets
time remaining into intervals, and reframes score/state in terms of the
leading team. Outputs a cleaned per-season CSV.

### 2_merge_datasets.R
Merges the cleaned 2022 and 2023 datasets into one combined training set.

### 3_super_learner.R
Trains a SuperLearner ensemble (GLM, ridge, tuned GAMs, etc.) to predict
whether the leading team wins, using time remaining and score differential.
Saves the fitted model(s) as `.rds` files.

### 4_plot_metrics.R
Loads a fitted SuperLearner model and generates diagnostic plots: learner
weights, predicted vs. raw win probabilities, calibration, ROC curves, and
cross-validated AUC.

### 5_test_dataset.R
Evaluates a fitted SuperLearner model on a held-out season (2021) as a test
set: ROC curve, GAM diagnostics, and residual simulation.

## Typical run order
```
0_get_pbp_data.R    (per season)
1_clean_data.R       (per season)
2_merge_datasets.R
3_super_learner.R
4_plot_metrics.R
5_test_dataset.R
```
