# Repository Release Roadmap

## Phase 1 - Research documentation

- [x] Study overview
- [x] Dataset roles
- [x] Experiment sequence
- [x] Configuration-lock documentation
- [x] Reported result summary
- [x] Citation metadata
- [ ] Software license selection

## Phase 2 - Original implementation sources

- [x] Publish original notebooks for the manuscript-facing 01C -> 08B flow
- [x] Publish multidomain 06A training notebook
- [x] Publish soft-routed residual-adapter 06D notebook
- [x] Publish 08A lock and 08B inference/evaluation notebooks
- [x] Add recorded package/environment specification
- [ ] Add any upstream source-model training material required to reproduce the frozen 01C checkpoints from scratch

## Phase 3 - Reproducibility artifacts

- [ ] Add public-ready lesion-safe source split manifests
- [ ] Add public-ready conventional split/audit manifests
- [ ] Add public-ready multidomain split manifests
- [x] Add label-harmonization documentation
- [x] Add frozen final configuration-lock record
- [x] Preserve checkpoint SHA256 identifiers in the lock record

## Phase 4 - Result artifacts

- [x] Add verified compact outputs for 01C
- [x] Add verified compact outputs for 04A
- [x] Add verified compact outputs for 05A
- [x] Add verified compact outputs for 06A
- [x] Add verified compact outputs for 06D
- [x] Add verified compact outputs for 08A
- [x] Add verified compact outputs for 08B
- [ ] Add publication figures to GitHub binary storage
- [ ] Add graphical abstract to GitHub binary storage
- [ ] Decide whether to publish sanitized per-image prediction tables
- [ ] Decide whether to distribute model checkpoints through a release/LFS/external archive

## Phase 5 - Verification

- [x] Cross-check headline metrics against frozen result archives
- [x] Audit seven notebooks for obvious credentials/tokens
- [ ] Fresh-environment setup test
- [ ] Public split-integrity reproduction test
- [ ] Inference smoke test using distributed model weights
- [ ] End-to-end metric reproduction from public artifacts
- [ ] Public release tag
