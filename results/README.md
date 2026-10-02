# Results

This directory contains verified compact result artifacts from the frozen experiment archives used for the manuscript.

## Published files

### 01C - lesion-safe source evaluation

- `table_primary_metrics_with_ci_and_comparison.csv`
- `per_class_metrics.csv`

### 04A - conventional image-level comparison

- `lesion_safe_vs_image_level.csv`
- `test_metrics_95ci.csv`
- `lesion_overlap_subgroups.csv`

### 05A - source-only external characterization

- `external_summary.csv`

### 06A - multidomain generalized baseline

- `generalized_validation_system_metrics.csv`

### 06D - soft-routed residual adaptation

- `baseline_vs_soft_routed_residual.csv`
- `router_behavior_selected_epoch.csv`

### 08A - final configuration lock

- `06D_vs_08A_validation.csv`
- `PAPEREXP08A_FINAL_GENERALIZED_CONFIGURATION_LOCK.json`

### 08B - post-lock DERM12345 evaluation

- `zero_shot_metrics.csv`
- `per_class_metrics.csv`
- `router_behavior.json`

The top-level `summary.csv` provides a compact overview of the manuscript-facing stages.

## Provenance

These files were checked against the uploaded frozen result archives rather than recreated from manuscript tables alone. Values are kept at the numerical precision available in the experiment outputs.

## Not currently published

Large checkpoints, recovery ZIP archives, and raw dataset images are excluded from normal Git history.

Per-image predictions are also withheld from this initial release while local runtime paths and redistribution fields are reviewed. Compact aggregate results are sufficient to audit the values reported in the manuscript, while the exact 08A lock preserves the model-component hashes needed for provenance.
