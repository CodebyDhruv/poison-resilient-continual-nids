# Project Context

## Objective

Build a final-year B.Tech research prototype for poison-resilient, novelty-aware continual learning in a Transformer-based Network Intrusion Detection System (NIDS).

The research question is whether an adaptive NIDS can retain known attack knowledge, learn new attack classes, and resist corrupted update data without rejecting every unfamiliar sample.

## Review-2 scope

This review prioritizes a basic, working demonstration over a final research contribution. The minimum pipeline is:

```text
CSV flow data -> preprocessing -> small tabular Transformer -> classification
         -> confidence novelty baseline -> Task 1 / Task 2 update
         -> label-flip poisoning comparison -> saved metrics
```

## Explicit baselines

- **Transformer:** a small tabular Transformer encoder is the classification backbone, not the novelty claim.
- **Novelty detection:** maximum-class-confidence threshold; this is a baseline only.
- **Continual learning:** sequential Task 1 to Task 2 training, with optional replay if stable in time.
- **Poisoning:** configurable label flipping of a bounded training fraction; it is not a claim to model every attacker.
- **Mitigation:** optional confidence- or anomaly-based filtering; do not delay the core pipeline to build it.

## Dataset decision

No dataset exists in the repository today. Do not automatically download one. For Review 2, use a documented, manageable flow-level CSV subset provided by the team (preferably CIC-IDS2017), with its source, fields, labels, split, and preprocessing recorded in `data/metadata/`.

Synthetic data may be used only for a component smoke test and must never be presented as NIDS evidence.

## Environment observed on 2026-10-02

- Python 3.14.6
- `numpy` and `pandas` are available.
- `torch` and `scikit-learn` are not installed.
- No dependency manifest, dataset, model, source implementation, or tests currently exist.

Dependency selection is pending. The first implementation owner must use versions compatible with the active Python runtime and record them in a shared dependency file.

## Research integrity

Use these terms accurately:

- **Hypothesis:** an expected outcome that has not been run.
- **Observed result:** metric produced by a recorded execution.
- **Baseline:** a comparison method, not a claimed contribution.
- **Not yet tested:** any unrun claim.
