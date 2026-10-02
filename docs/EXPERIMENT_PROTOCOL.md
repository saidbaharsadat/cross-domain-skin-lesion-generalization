# Experiment Protocol

The repository follows the experimental sequence used in the manuscript.

## 01C - Lesion-safe source evaluation

Purpose:
- evaluate the source EfficientNet-B0/B3 ensemble on the native seven-class HAM10000 task;
- use lesion-grouped partitions;
- establish a leakage-controlled internal reference.

Held-out test:
- 971 images;
- 749 lesion groups.

Reported performance:
- accuracy: 86.82%;
- Macro-F1: 0.7333;
- balanced accuracy: 0.7076;
- MEL recall: 75.24%;
- Macro-AUC: 0.9756.

## 04A - Conventional image-level comparison

Purpose:
- provide an intentionally conventional image-level comparison;
- audit lesion identity overlap.

Reported performance:
- accuracy: 91.35%;
- Macro-F1: 0.8676;
- balanced accuracy: 0.8647;
- MEL recall: 80.56%;
- Macro-AUC: 0.9877.

Lesion-identity audit:
- 402 / 971 test images (41.40%) shared lesion identity with training or validation;
- 372 / 971 (38.31%) shared lesion identity specifically with training;
- no duplicate file/pixel overlap was detected.

Because the lesion-safe and conventional protocols use different partitions, the performance difference is descriptive rather than a paired causal estimate of leakage inflation.

## 05A - Source-only zero-shot characterization

A frozen native seven-class source model was evaluated without target-domain adaptation on:
- DERM12345;
- Derm7pt;
- BCN20000;
- PAD-UFES-20.

For five-class external cohorts, DF/VASC predictions were counted as incorrect and probabilities were not renormalized.

Equal-domain summary:
- accuracy: 61.90%;
- Macro-F1: 0.4413;
- balanced accuracy: 0.4565;
- MEL recall: 36.40%;
- Macro-AUC: 0.8317.

## 06A - Five-class multidomain baseline

Architecture:
- 3 x EfficientNet-B0;
- 3 x EfficientNet-B3;
- 300 x 300 inputs;
- eight training epochs;
- hierarchical domain -> class -> image sampling.

Reported equal-domain development-validation performance:
- accuracy: 79.88%;
- Macro-F1: 0.7538;
- balanced accuracy: 0.7662;
- MEL recall: 69.49%;
- Macro-AUC: 0.9475.

## 06D - Frozen-backbone soft-routed residual adaptation

The six 06A classifiers are frozen.

With residual gain alpha = 1.0:
- accuracy: 81.58%;
- Macro-F1: 0.7722;
- balanced accuracy: 0.7672;
- MEL recall: 69.19%;
- Macro-AUC: 0.9491.

## 08A - Final generalized configuration

Development validation selected residual gain alpha = 1.05.

Locked components:
- six frozen classifiers;
- three residual adapters;
- epoch-3 adapter checkpoints;
- four experts per adapter;
- TTA7;
- equal B0/B3 family fusion;
- argmax classification;
- residual gain alpha = 1.05.

Reported equal-domain development-validation performance:
- accuracy: 81.64%;
- Macro-F1: 0.7732;
- balanced accuracy: 0.7676;
- MEL recall: 69.23%;
- Macro-AUC: 0.9491.

## Configuration-lock boundary

After 08A was selected, the final generalized configuration was locked.

DERM12345 labels and outcomes were not used for:
- generalized-model training;
- residual adaptation;
- checkpoint selection;
- calibration;
- threshold optimization;
- ensemble-weight optimization;
- TTA selection;
- residual-gain selection.

## 08B - Post-lock DERM12345 evaluation

Cohort:
- 2,321 images;
- 574 groups.

Reported performance:
- accuracy: 92.55%;
- Macro-F1: 0.6985;
- balanced accuracy: 0.7487;
- MEL recall: 76.83%;
- Macro-AUC: 0.9683.

The cohort had previously been inspected through source-only 05A characterization. Therefore, 08B is described as a post-lock zero-shot evaluation of the generalized model, not as a cohort that was wholly unseen throughout the research project.
