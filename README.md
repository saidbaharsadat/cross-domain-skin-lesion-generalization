# Cross-Domain Generalization for Skin Lesion Classification with Soft-Routed Residual Adaptation

Research repository for the manuscript:

**Said Bahar Sadat and Chen Kesong, "Cross-Domain Generalization for Skin Lesion Classification with Soft-Routed Residual Adaptation."**

**Status:** Submitted to the *IEEE Journal of Biomedical and Health Informatics (JBHI)* and currently under review.

> This repository is being organized as the public reproducibility companion to the manuscript. The current repository release documents the study design, dataset roles, locked evaluation protocol, label space, and reported results. The executable training and evaluation code will be added from the original experiment sources rather than reconstructed from the paper.

## Overview

Skin-lesion classifiers can perform strongly on internal data while degrading when acquisition conditions, devices, populations, or dataset conventions change. Evaluation can also be optimistic when multiple images of the same lesion are split across training and testing.

This work studies both problems through:

- lesion- and group-aware evaluation;
- source-only cross-domain characterization;
- a six-model EfficientNet-B0/B3 multidomain ensemble;
- frozen-backbone soft-routed residual adaptation;
- bounded prediction corrections;
- image-conditioned routing without dataset identity at inference; and
- a locked post-development evaluation on a predefined DERM12345 cohort without target-domain adaptation.

## Study design

The experimental sequence is:

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

The seven-class source experiments and the five-class multidomain experiments serve different purposes and should not be treated as a controlled architecture-only comparison.

## Datasets and roles

| Dataset | Modality | Study role |
|---|---|---|
| ISIC2018 / HAM10000 | Dermoscopic | Native 7-class source task and 5-class multidomain development |
| BCN20000 | Dermoscopic | Source-only characterization and multidomain development |
| Derm7pt | Dermoscopic | Source-only characterization and multidomain development |
| PAD-UFES-20 | Clinical smartphone | Source-only characterization and multidomain development |
| DERM12345 | Dermoscopic | Source-only characterization and predefined post-lock 08B evaluation |

The four-domain multidomain development split contains **16,220 training images** and **3,895 validation images**. Development partitions are image-disjoint and group-disjoint within each domain.

The predefined DERM12345 08B cohort contains **2,321 images from 574 groups**.

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

## Model

The generalized base consists of:

- 3 x EfficientNet-B0 classifiers;
- 3 x EfficientNet-B3 classifiers;
- 300 x 300 model inputs for the five-class generalized baseline;
- equal averaging within each architecture family;
- 0.5 / 0.5 B0-B3 probability fusion.

During residual specialization, all six base classifiers are frozen.

Each residual adapter uses:

- mean B0 feature: 1,280 -> 64;
- mean B3 feature: 1,536 -> 64;
- 26-dimensional prediction-statistics vector -> 32;
- concatenated 160-dimensional representation;
- shared 128-dimensional representation;
- four-way soft routing;
- four bounded residual experts.

Three independently trained residual adapters are averaged. The final locked gain is **alpha = 1.05**.

Dataset identity is **not** supplied at validation or inference.

## Main reported results

### Lesion-safe native source evaluation

| Metric | Result |
|---|---:|
| Accuracy | 86.82% |
| Macro-F1 | 0.7333 |
| Balanced accuracy | 0.7076 |
| Melanoma recall | 75.24% |
| Macro-AUC | 0.9756 |

The conventional image-level comparison reached 91.35% accuracy, but **402 / 971 test images (41.40%)** shared lesion identity with training or validation.

### Five-class multidomain development

| Configuration | Accuracy | Macro-F1 | Balanced acc. | MEL recall | Macro-AUC |
|---|---:|---:|---:|---:|---:|
| 06A generalized baseline | 79.88% | 0.7538 | 0.7662 | 69.49% | 0.9475 |
| 06D soft-routed residual | 81.58% | 0.7722 | 0.7672 | 69.19% | 0.9491 |
| 08A final locked configuration | **81.64%** | **0.7732** | **0.7676** | 69.23% | **0.9491** |

These are equal-domain development-validation results and are descriptive rather than independent final-test estimates.

### Post-lock DERM12345 evaluation

The exact locked 08A configuration was applied to the predefined 08B DERM12345 cohort without target-domain adaptation.

| Metric | Result |
|---|---:|
| Accuracy | **92.55%** |
| Macro-F1 | **0.6985** |
| Balanced accuracy | **0.7487** |
| Melanoma recall | **76.83%** |
| Macro-AUC | **0.9683** |

DERM12345 had previously been inspected in the source-only characterization stage, but its outcomes were not used to train, calibrate, select, or tune the final generalized configuration.

## Repository layout

```text
.
├── README.md
├── CITATION.cff
├── .gitignore
├── docs/
│   ├── DATASETS.md
│   ├── EXPERIMENT_PROTOCOL.md
│   ├── REPRODUCIBILITY.md
│   └── REPOSITORY_ROADMAP.md
├── metadata/
│   └── LABEL_HARMONIZATION.md
├── src/
│   └── README.md
├── scripts/
│   └── README.md
├── configs/
│   └── README.md
├── splits/
│   └── README.md
├── results/
│   ├── README.md
│   └── summary.csv
└── figures/
    └── README.md
```

## Data

The original images are **not redistributed** in this repository.

All datasets analyzed in the study are publicly available from their original providers. This repository is intended to contain derived split manifests, label-harmonization information, experiment configuration, and reproducibility metadata only.

See [docs/DATASETS.md](docs/DATASETS.md).

## Reproducibility

The public release is being organized around the exact experimental sequence and configuration-lock boundary used in the manuscript. We will not replace missing historical implementation details with newly invented equivalents.

See [docs/REPRODUCIBILITY.md](docs/REPRODUCIBILITY.md).

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

The manuscript is under peer review. Results in this repository should be interpreted as research findings from a retrospective study, not as evidence of clinical safety or readiness for deployment.

## License

A software license has not yet been selected for the code release. Until a LICENSE file is added, do not assume permission to reuse repository contents beyond rights provided by applicable law.
