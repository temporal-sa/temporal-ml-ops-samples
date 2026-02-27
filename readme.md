# Temporal ML Ops Samples

This repo, temporal-ml-ops-samples, is a set of Python examples showing how to use Temporal for durable ML operations. It focuses on BERT fine‑tuning and inference with Hugging Face Transformers/Datasets, and it separates deterministic orchestration (workflows) from non‑deterministic ML work (activities). The code is organized under ml_ops/ with clear entrypoints, workers, and Pydantic models to keep workflow inputs/outputs explicit and replay‑safe.

The ml_ops/durable_training module demonstrates checkpoint‑aware fine‑tuning and resumable inference. It includes a Temporal worker, a CLI starter, and tests, plus docs on architecture and comparisons with other orchestrators. The key idea is that training can be interrupted and resumed from the latest checkpoint rather than restarting from scratch, which makes long‑running runs robust and cost‑efficient.

The ml_ops/hyperparam_optimization module builds on the same foundation to run durable hyperparameter sweeps (ladder and TPE‑style) as pure workflows. It splits training and evaluation across separate task queues, keeps randomness deterministic, and tracks trial results to guide later configs. There’s a starter script and notebook to kick off sweeps locally, making it a solid reference for production‑grade, fault‑tolerant ML orchestration patterns.

## Where To Go

- `ml_ops/` — primary samples and reference implementations. See the breakdown below.

## ml_ops Breakdown

- `ml_ops/durable_training/` — durable training sample. Start with `README.md`, then look at `starter.py`, `worker.py`, and `workflows.py`.
- `ml_ops/hyperparam_optimization/` — hyperparameter sweep sample. Start with `README.md`, then look at `starter.py`, `training_worker.py`, and `workflows.py`.
- In both samples, `docs/` contains architecture and competitive comparison writeups, and `tests/` contains workflow/activity tests.