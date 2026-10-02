# Label Harmonization

## Source task

The native HAM10000 source task retains seven classes:

| Code | Class |
|---|---|
| MEL | Melanoma |
| NV | Melanocytic nevus |
| BCC | Basal cell carcinoma |
| AKIEC | Actinic keratosis / intraepithelial carcinoma |
| BKL | Benign keratosis-like lesion |
| DF | Dermatofibroma |
| VASC | Vascular lesion |

## Multidomain task

The multidomain task retains five classes:

| Code | Class |
|---|---|
| MEL | Melanoma |
| NV | Melanocytic nevus |
| BCC | Basal cell carcinoma |
| AKIEC | Actinic keratosis / intraepithelial carcinoma |
| BKL | Benign keratosis-like lesion |

DF and VASC are excluded from multidomain development because defensible equivalent categories are not consistently available across the participating domains.

## PAD-UFES-20 mappings explicitly reported in the manuscript

| PAD-UFES-20 label | Harmonized label |
|---|---|
| MEL | MEL |
| NEV | NV |
| BCC | BCC |
| ACK | AKIEC |
| SEK | BKL |
| SCC | Excluded |

Additional dataset-specific raw-label mappings should be added only from the actual preprocessing manifests or original code.
