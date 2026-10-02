# Reproducibility Policy

The goal of this repository is to expose the experiment logic and derived artifacts required to reproduce the manuscript as faithfully as possible.

## Release principles

1. **Do not reconstruct missing historical code from memory.**
   Public code should come from the original experiment sources or be explicitly labeled as a later refactor.

2. **Preserve the accepted experiment sequence.**
   The study sequence is 01C -> 04A -> 05A -> 06A -> 06D -> 08A -> 08B.

3. **Preserve the configuration-lock boundary.**
   The final 08A configuration was locked before 08B evaluation.

4. **Keep source and multidomain tasks separate.**
   The source stage uses seven classes; multidomain development uses the harmonized five-class task.

5. **Do not redistribute original dataset images.**
   Dataset acquisition remains the responsibility of the user through the original providers.

6. **Publish derived split manifests where permitted.**
   Lesion/group identifiers and split assignments are central to the leakage-control claims and should be versioned.

7. **Preserve exact metrics and evaluation definitions.**
   Equal-domain development metrics average domain-level metrics with one-quarter weight per development domain.

## Artifacts planned for release

- source lesion-safe split manifests;
- conventional split/audit metadata;
- five-class multidomain split manifests;
- label-harmonization files;
- model configuration files;
- training scripts;
- residual-adapter implementation;
- inference scripts;
- evaluation scripts;
- frozen result summaries;
- environment/package information;
- configuration-lock record.

## Items intentionally excluded

- original public-dataset image files;
- private credentials or API keys;
- journal submission-system files;
- signed author-consent forms;
- personal local paths;
- temporary checkpoints not required for reproducibility.

## Evaluation cautions

- 08A metrics are development-validation evidence, not independent final-test estimates.
- 08B is a single retrospective post-lock cohort.
- DERM12345 was used earlier for source-only characterization, but not for selecting or tuning 08A.
- The study does not establish prospective clinical safety.
