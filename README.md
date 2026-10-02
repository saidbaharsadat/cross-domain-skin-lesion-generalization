# Cross-Domain Generalization for Skin Lesion Classification with Soft-Routed Residual Adaptation

Public research and reproducibility repository for the manuscript:

**Said Bahar Sadat and Chen Kesong, "Cross-Domain Generalization for Skin Lesion Classification with Soft-Routed Residual Adaptation."**

**Status:** Submitted to the *IEEE Journal of Biomedical and Health Informatics (JBHI)* and currently under review.

> The repository preserves the accepted experiment sequence and publishes the original Kaggle notebooks for the manuscript-facing experiments together with verified result tables, the final configuration-lock record, environment information, and study documentation. Original dataset images are not redistributed.

## Overview

Skin-lesion classifiers can perform strongly on internal data while degrading when acquisition conditions, devices, populations, or dataset conventions change. Evaluation can also be optimistic when multiple images of the same lesion cross an image-level train/test boundary.

This study investigates both issues through:

- lesion- and group-aware evaluation;
- an explicit lesion-overlap audit of conventional image-level splitting;
- source-only cross-domain characterization;
- a six-model EfficientNet-B0/B3 multidomain ensemble;
- frozen-backbone soft-routed residual adaptation;
- bounded image-conditioned prediction corrections;
- routing without dataset identity at inference; and
- a locked post-development evaluation on a predefined DERM12345 cohort without target-domain adaptation.

## Experiment flow

```text
01C  Lesion-safe source evaluation
 |
04A  Conventional image-level comparison + lesion-overlap audit
 |
05A  Frozen source-only zero-shot characterization
 |
06A  Five-class multidomain generalized baseline
 |
06D  Frozen-backbone soft-routed residual adaptation
 |
08A  Final configuration selection and lock
 |
08B  Post-lock evaluation on DERM12345
```

The original notebooks for all seven stages are available in [notebooks/](notebooks/).

The seven-class source task and five-class multidomain task have different scientific roles. Numerical differences across those task spaces are not treated as controlled architecture-only comparisons.

## Public artifacts

### Original experiment notebooks

| Stage | Notebook | Purpose |
|---|---|---|
| 01C | [01C_source_lesion_safe.ipynb](notebooks/01C_source_lesion_safe.ipynb) | Frozen lesion-safe internal evaluation |
| 04A | [04A_conventional_image_level.ipynb](notebooks/04A_conventional_image_level.ipynb) | Conventional image-level comparison and overlap audit |
| 05A | [05A_source_only_external.ipynb](notebooks/05A_source_only_external.ipynb) | Frozen source-only external characterization |
| 06A | [06A_multidomain_baseline.ipynb](notebooks/06A_multidomain_baseline.ipynb) | Five-class multidomain baseline |
| 06D | [06D_soft_routed_residual.ipynb](notebooks/06D_soft_routed_residual.ipynb) | Frozen-backbone residual adaptation |
| 08A | [08A_final_configuration_lock.ipynb](notebooks/08A_final_configuration_lock.ipynb) | Final gain selection and configuration lock |
| 08B | [08B_derm12345_post_lock.ipynb](notebooks/08B_derm12345_post_lock.ipynb) | Post-lock DERM12345 evaluation |

These are provenance-preserving Kaggle notebooks. They retain original Kaggle paths and execution outputs. Dataset paths must therefore be adapted when running outside the original environment.

### Verified result artifacts

Compact result files copied from or checked against the frozen experiment archives are available under [results/](results/), including:

- 01C primary metrics, lesion-bootstrap confidence intervals, and per-class metrics;
- 04A conventional image-level metrics and lesion-overlap subgroup analysis;
- 05A external-domain summary;
- 06A multidomain validation metrics;
- 06D baseline comparison and router behavior;
- 08A validation comparison and the exact final configuration-lock record;
- 08B DERM12345 overall, class-level, and router results.

Large model checkpoints and original dataset images are intentionally not stored in normal Git history.

## Datasets and roles

| Dataset | Modality | Study role |
|---|---|---|
| ISIC2018 / HAM10000 | Dermoscopic | Native 7-class source task and 5-class multidomain development |
| BCN20000 | Dermoscopic | Source-only characterization and multidomain development |
| Derm7pt | Dermoscopic | Source-only characterization and multidomain development |
| PAD-UFES-20 | Clinical smartphone | Source-only characterization and multidomain development |
| DERM12345 | Dermoscopic | Source-only characterization and predefined post-lock 08B evaluation |

The four-domain multidomain development split contains **16,220 training images** and **3,895 validation images**. The recorded development audit reports zero image overlap and zero group overlap between training and validation within each development domain.

The predefined DERM12345 08B cohort contains **2,321 images from 574 groups**.

See [docs/DATASETS.md](docs/DATASETS.md).

## Diagnostic spaces

### Native seven-class source task

- MEL - melanoma
- NV - melanocytic nevus
- BCC - basal cell carcinoma
- AKIEC - actinic keratosis / intraepithelial carcinoma
- BKL - benign keratosis-like lesion
- DF - dermatofibroma
- VASC - vascular lesion

### Harmonized five-class multidomain task

- MEL
- NV
- BCC
- AKIEC
- BKL

For PAD-UFES-20, the mappings explicitly used in the manuscript are **NEV -> NV**, **ACK -> AKIEC**, and **SEK -> BKL**; SCC is excluded from the harmonized five-class task.

See [metadata/LABEL_HARMONIZATION.md](metadata/LABEL_HARMONIZATION.md).

## Model

The generalized base consists of:

- 3 x EfficientNet-B0 classifiers;
- 3 x EfficientNet-B3 classifiers;
- 300 x 300 inputs;
- equal probability averaging within each architecture family;
- fixed 0.5 / 0.5 B0-B3 family fusion.

During residual specialization, all six base classifiers are frozen.

Each residual adapter uses:

- mean B0 feature: 1,280 -> 64;
- mean B3 feature: 1,536 -> 64;
- 26-dimensional prediction-statistics vector -> 32;
- concatenated 160-dimensional representation;
- shared 128-dimensional representation;
- four-way soft routing;
- four bounded residual experts.

Three independently trained residual adapters are averaged. The final locked gain is **alpha = 1.05**. Dataset identity is not supplied during validation or inference.

## Main reported results

### 01C - lesion-safe source evaluation

| Metric | Result |
|---|---:|
| Accuracy | 86.82% |
| Macro-F1 | 0.7333 |
| Balanced accuracy | 0.7076 |
| Melanoma recall | 75.24% |
| Macro-AUC | 0.9756 |

The held-out lesion-safe test contains **971 images from 749 lesion groups**.

### 04A - conventional image-level comparison

The conventional image-level comparison reached **91.35% accuracy** and **0.8676 Macro-F1**. Its lesion-identity audit found that **402 / 971 test images (41.40%)** shared lesion identity with training or validation, including **372 / 971 (38.31%)** with training.

Because 01C and 04A use different partitions, their performance difference is descriptive rather than a paired causal estimate of leakage inflation.

### 05A - source-only external characterization

| Metric | Equal-domain mean |
|---|---:|
| Accuracy | 61.90% |
| Macro-F1 | 0.4413 |
| Balanced accuracy | 0.4565 |
| Melanoma recall | 36.40% |
| Macro-AUC | 0.8317 |

The frozen native seven-class source model was applied without target adaptation. For harmonized five-class external cohorts, predictions to DF or VASC were counted as incorrect and probabilities were not renormalized.

### 06A -> 06D -> 08A multidomain development

| Configuration | Accuracy | Macro-F1 | Balanced acc. | MEL recall | Macro-AUC |
|---|---:|---:|---:|---:|---:|
| 06A generalized baseline | 79.88% | 0.7538 | 0.7662 | 69.49% | 0.9475 |
| 06D soft-routed residual | 81.58% | 0.7722 | 0.7672 | 69.19% | 0.9491 |
| 08A final locked configuration | **81.64%** | **0.7732** | **0.7676** | 69.23% | **0.9491** |

These are equal-domain development-validation results and are not independent final-test estimates.

The exact 08A lock is preserved in [results/08A/PAPEREXP08A_FINAL_GENERALIZED_CONFIGURATION_LOCK.json](results/08A/PAPEREXP08A_FINAL_GENERALIZED_CONFIGURATION_LOCK.json).

### 08B - post-lock DERM12345 evaluation

The exact locked 08A model was applied to the predefined DERM12345 cohort without target-domain adaptation.

| Metric | Result |
|---|---:|
| Accuracy | **92.55%** |
| Macro-F1 | **0.6985** |
| Balanced accuracy | **0.7487** |
| Melanoma recall | **76.83%** |
| Macro-AUC | **0.9683** |

DERM12345 had previously been inspected during 05A source-only characterization. Its outcomes did not train, calibrate, select, or tune the final 08A generalized configuration. Accordingly, 08B is described as a **post-lock zero-shot evaluation**, not as a dataset wholly unseen throughout the entire research project.

For transparency, the frozen 08B archive also records descriptive 06A-parent and 06D-gain-1.00 predictions computed in the same once-opened DERM12345 run. They are included in [results/08B/zero_shot_metrics.csv](results/08B/zero_shot_metrics.csv) and should not be interpreted as independently pre-registered external comparisons.

## Reference environment

The experiment audit recorded:

- Python 3.12.13
- PyTorch 2.10.0+cu128
- torchvision 0.25.0+cu128
- NumPy 2.0.2
- pandas 2.3.3
- scikit-learn 1.6.1
- NVIDIA Tesla T4

See [requirements.txt](requirements.txt) and [environment/README.md](environment/README.md).

## Repository layout

```text
.
├── README.md
├── CITATION.cff
├── requirements.txt
├── .gitignore
├── notebooks/
│   ├── 01C_source_lesion_safe.ipynb
│   ├── 04A_conventional_image_level.ipynb
│   ├── 05A_source_only_external.ipynb
│   ├── 06A_multidomain_baseline.ipynb
│   ├── 06D_soft_routed_residual.ipynb
│   ├── 08A_final_configuration_lock.ipynb
│   └── 08B_derm12345_post_lock.ipynb
├── results/
│   ├── 01C/
│   ├── 04A/
│   ├── 05A/
│   ├── 06A/
│   ├── 06D/
│   ├── 08A/
│   └── 08B/
├── docs/
├── metadata/
├── environment/
├── splits/
├── configs/
├── figures/
├── src/
└── scripts/
```

## Data and privacy

Original dataset images are **not redistributed** in this repository.

The public repository also intentionally excludes:

- the JBHI reviewer/submission-system PDF;
- signed author-consent forms;
- submission identifiers and private journal correspondence;
- credentials and authentication tokens;
- local private files;
- temporary checkpoints not required in normal Git history.

Derived split manifests will be added only after verifying that their fields and redistribution conditions are appropriate for public release.

## Reproducibility scope

The original manuscript-facing experiment notebooks and verified compact outputs are now public. Some upstream recovery materials, source-model training provenance, public-ready split manifests, and large model checkpoints are still being prepared separately. The repository therefore documents the current reproducibility boundary explicitly rather than reconstructing missing historical material.

See [docs/EXPERIMENT_PROTOCOL.md](docs/EXPERIMENT_PROTOCOL.md), [docs/REPRODUCIBILITY.md](docs/REPRODUCIBILITY.md), and [docs/REPOSITORY_ROADMAP.md](docs/REPOSITORY_ROADMAP.md).

## Citation

Citation metadata is provided in [CITATION.cff](CITATION.cff).

Until a final journal citation is available, please cite the manuscript title and this repository.

## Authors

**Said Bahar Sadat**  
School of Information and Communication Engineering  
University of Electronic Science and Technology of China (UESTC)  
ORCID: https://orcid.org/0009-0002-0961-882X

**Chen Kesong**  
School of Information and Communication Engineering  
University of Electronic Science and Technology of China (UESTC)

## Publication status

The manuscript is under peer review. Results in this repository are retrospective research findings and do not establish clinical safety or readiness for clinical deployment.

## License

A software license has not yet been selected. Until a LICENSE file is added, do not assume permission to reuse repository contents beyond rights provided by applicable law.
