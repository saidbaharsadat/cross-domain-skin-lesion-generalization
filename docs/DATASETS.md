# Datasets and Study Roles

This document records the dataset roles reported in the manuscript. Original dataset images are not redistributed by this repository.

## Datasets

### ISIC2018 / HAM10000

Role:
- native seven-class source task;
- source lesion-safe evaluation;
- conventional image-level comparison;
- five-class multidomain development.

HAM10000 contains 10,015 dermoscopic images in its native seven-class taxonomy.

Primary lesion-safe source partitions:
- training: 6,828 images / 5,111 lesion groups;
- validation: 1,464 images / 1,093 lesion groups;
- held-out lesion-safe test: 971 images / 749 lesion groups.

Five-class multidomain partition:
- training: 7,793 images;
- validation: 1,020 images.

### BCN20000

Role:
- frozen source-only characterization;
- five-class multidomain development.

Five-class development partition:
- training: 6,957 images;
- validation: 2,387 images;
- group-disjoint within the development protocol.

### Derm7pt

Role:
- frozen source-only characterization;
- five-class multidomain development.

Five-class development partition:
- training: 213 images;
- validation: 71 images;
- group-disjoint within the development protocol.

### PAD-UFES-20

Role:
- frozen source-only characterization;
- five-class multidomain development.

Modality: clinical smartphone images.

Five-class development partition:
- training: 1,257 images;
- validation: 417 images;
- patient/group-disjoint within the development protocol.

Explicit manuscript label mappings:
- NEV -> NV
- ACK -> AKIEC
- SEK -> BKL
- MEL -> MEL
- BCC -> BCC
- SCC excluded from the harmonized five-class task

### DERM12345

Role:
- source-only characterization in 05A;
- post-lock evaluation of the final generalized model in 08B.

Predefined 08B cohort:
- 2,321 images;
- 574 groups;
- 82 MEL;
- 2,000 NV;
- 85 BCC;
- 19 AKIEC;
- 135 BKL.

DERM12345 outcomes were not used to train, adapt, calibrate, select, or tune the final generalized configuration.

## Four-domain multidomain development total

- training: 16,220 images;
- validation: 3,895 images.

The predefined multidomain training and validation partitions are image-disjoint and group-disjoint within each domain.

## Data access

Users should obtain each dataset from its original public provider and comply with the provider's access terms, citation requirements, and license conditions.

This repository will store only derived metadata needed for reproducibility, such as split manifests and harmonized labels, where redistribution is permitted.
