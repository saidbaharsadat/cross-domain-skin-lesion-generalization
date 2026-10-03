# v1.0-submission

Initial public research release corresponding to the manuscript submission:

**Cross-Domain Generalization for Skin Lesion Classification with Soft-Routed Residual Adaptation**

Authors: Said Bahar Sadat and Chen Kesong

Manuscript status at release: submitted to the *IEEE Journal of Biomedical and Health Informatics (JBHI)* and under review.

## Included

- Original Kaggle notebooks for the accepted manuscript-facing experiment sequence:
  - 01C lesion-safe source evaluation
  - 04A conventional image-level comparison and lesion-overlap audit
  - 05A source-only external characterization
  - 06A five-class multidomain generalized baseline
  - 06D frozen-backbone soft-routed residual adaptation
  - 08A final configuration selection and lock
  - 08B post-lock DERM12345 evaluation
- Verified compact result artifacts for all seven stages.
- Exact 08A final configuration-lock record and checkpoint SHA256 identifiers.
- Environment and package information recorded from the experiment runtime.
- Dataset-role and label-harmonization documentation.
- Final manuscript figures and graphical abstract.
- CITATION.cff metadata.
- MIT software license.

## Headline results

- 01C lesion-safe source test: 86.82% accuracy, 0.7333 Macro-F1.
- 06A equal-domain development validation: 79.88% accuracy, 0.7538 Macro-F1.
- 06D soft-routed residual: 81.58% accuracy, 0.7722 Macro-F1.
- 08A final locked configuration: 81.64% accuracy, 0.7732 Macro-F1.
- 08B post-lock DERM12345: 92.55% accuracy, 0.6985 Macro-F1, 76.83% melanoma recall.

## Scientific boundaries

- The source-stage seven-class experiments and multidomain five-class experiments have different roles and are not treated as controlled architecture-only comparisons.
- 08A metrics are development-validation results used to select and lock the final generalized configuration; they are not independent final-test estimates.
- DERM12345 was previously inspected during 05A source-only characterization, but its outcomes did not train, calibrate, select, or tune the final 08A configuration. 08B is therefore described as post-lock zero-shot evaluation rather than a dataset wholly unseen throughout the project.
- Original dataset images are not redistributed.
- The JBHI reviewer/submission package, signed consent form, submission identifiers, and private journal correspondence are excluded.

## Not included in this release

- Original public-dataset image files.
- Large model checkpoints in normal Git history.
- Private journal-administration files.
- Public-ready split manifests and sanitized per-image prediction tables are still under review for a later reproducibility update.

This release is a research artifact and does not establish clinical safety or readiness for clinical deployment.
