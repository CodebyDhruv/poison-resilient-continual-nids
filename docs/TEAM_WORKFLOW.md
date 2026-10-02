# Team Workflow

## Ownership

| Area | Primary owner | Supporting owner | First responsibility |
| --- | --- | --- | --- |
| Data and preprocessing | Member 1 | Member 4 | Dataset audit and repeatable task streams |
| Transformer NIDS | Member 2 | Member 1 | Static baseline and training loop |
| Continual learning and novelty | Member 3 | Member 2 | Replay buffer, forgetting, quarantine |
| Poison resilience and integration | Member 4 | Member 3 | Attack harness, defense evaluation, orchestration |

Replace the member placeholders with GitHub usernames after the team is added as collaborators.

## Branch and pull request rules

- Create one issue per meaningful task.
- Use short branch names: `data/...`, `model/...`, `cl/...`, `poison/...`, `eval/...`, `docs/...`.
- Keep pull requests focused and small enough to review.
- Do not merge code that changes the experimental protocol without updating `docs/PROJECT_BLUEPRINT.md`.
- At least one teammate should review code that affects shared interfaces or experimental claims.
- Never commit datasets, checkpoints, secrets, or manually edited result files.

## Experiment record

Every result must record:

```text
experiment name:
git commit:
dataset and version:
task stream / split:
seed(s):
model and key hyperparameters:
attack and poison budget (if any):
defense configuration (if any):
metrics location:
observed result:
limitations:
```

## Meeting cadence

- Weekly: 20-minute integration check - blockers, interface changes, next experiment.
- Before each review: freeze the experiment plan, rerun priority configurations, then prepare slides/demo.
- Any surprising result is discussed before changing the methodology.
