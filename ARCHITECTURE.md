# Review-2 Architecture and Interfaces

## Current architecture

No implementation exists yet. This document freezes the smallest interface contract needed for parallel work. Changes require Developer B's integration approval.

```text
Developer B: data + task stream
    PreparedDataset / IncrementalTask
              |
              v
Developer A: Transformer model <---- replay batches from Developer B
    predicted labels + probabilities
              |
              +--> Developer C: novelty, poisoning, metrics
              |
              v
Developer B: one-command integration and saved result manifest
```

## Canonical data contract

`src/data/` will expose a prepared dataset/task with these fields:

```python
features: numpy.ndarray       # shape (n_samples, n_features), float32
labels: numpy.ndarray         # shape (n_samples,), integer class IDs
feature_names: list[str]      # fixed feature order
class_names: dict[int, str]   # ID-to-label mapping
```

The data owner is responsible for fitting preprocessing on the training partition only and applying the same transform to validation/test partitions. Task definitions must record included classes, row counts, and seed.

## Model contract

`src/models/` will provide a classifier with:

```python
fit(X_train, y_train, X_val=None, y_val=None, replay=None) -> TrainingHistory
predict(X) -> numpy.ndarray                 # integer class IDs
predict_proba(X) -> numpy.ndarray           # shape (n_samples, n_known_classes)
save(path) -> None
load(path) -> Classifier
```

`predict_proba` columns must stay aligned with the exposed `class_ids` property. The model owner must support a tiny CPU smoke run before full training.

## Novelty contract

`src/novelty/` will consume model probabilities only:

```python
detect_unknown(probabilities, threshold) -> numpy.ndarray  # bool mask
```

The Review-2 baseline is `max(probabilities) < threshold`. The function must not modify the model or input arrays.

## Poisoning contract

`src/poisoning/` will expose:

```python
apply_label_flip(labels, rate, seed, allowed_classes=None) -> PoisoningResult
```

The result contains changed labels, changed row indices, requested rate, achieved rate, and seed. Original labels must remain available for evaluation.

## Evaluation contract

`src/evaluation/` will expose functions that return JSON-serializable dictionaries:

```python
classification_metrics(y_true, y_pred) -> dict
continual_metrics(task1_before, task1_after, task2_score) -> dict
novelty_metrics(is_unknown_true, is_unknown_pred) -> dict
```

## Integration contract

`run_pipeline.py` (owned by Developer B) will accept one config, invoke components in order, print only observed values, and save a timestamped JSON result manifest under `results/`. It must support a small CPU smoke configuration before a larger dataset run.
