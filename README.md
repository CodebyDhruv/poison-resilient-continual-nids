# Poison-Resilient Continual NIDS

Research prototype for **poison-resilient, novelty-aware continual learning** in a Transformer-based Network Intrusion Detection System (NIDS).

The project asks a focused question: can replay-based continual learning retain prior attack knowledge and learn genuine new attacks while resisting corrupted update data?

## Project scope

This is a semester-scale research prototype - not a production IDS or SIEM.

The core pipeline is:

```text
Flow dataset -> preprocessing -> Transformer classifier -> replay memory
                                                     -> secure admission gate
                                                     -> quarantine / re-audit
                                                     -> continual update
```

## Minimum research target

1. Build a reproducible tabular Transformer baseline.
2. Compare static training, sequential fine-tuning, and replay-based continual learning.
3. Simulate label-flip poisoning in incoming/replay candidates.
4. Evaluate at least one lightweight replay-admission defense.
5. Report detection quality, forgetting, poison admission, and legitimate-new-class acceptance.

The timing-feature backdoor, CI/CII streams, periodic buffer audit, and a secondary dataset are strong extensions after the minimum target works.

## Repository map

| Path | Purpose |
| --- | --- |
| `src/` | Reusable implementation modules. |
| `configs/` | Versioned experiment configurations. |
| `experiments/` | Runnable experiment entry points and notes. |
| `tests/` | Unit and integration tests. |
| `docs/` | Research, workflow, and decision documentation. |
| `data/` | Local data layout only; datasets are ignored by Git. |
| `results/` | Generated metrics and figures; raw outputs are ignored by Git. |

## Getting started

1. Read [the project blueprint](docs/PROJECT_BLUEPRINT.md) and [team workflow](docs/TEAM_WORKFLOW.md).
2. Create an issue before beginning a non-trivial piece of work.
3. Work in a focused branch, for example `data/cicids-preprocessing`.
4. Open a pull request using the provided template.
5. Record every experiment's configuration, dataset version, seed, and result location.

## Research integrity

Never fabricate results or present unrun experiments as findings. Clearly mark outcomes as **hypotheses**, **expected results**, or **observed results**. A defense that rejects all unfamiliar traffic does not satisfy the novelty-learning objective.

## Current status

Blueprint only. No dataset, model, or experiment has been implemented yet.
