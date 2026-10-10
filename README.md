# DeltaNLP — Agenthon Track 1 Coding

Runtime House-model agent for quantitative-finance programming. This candidate has **no official solve rate yet**. It contains no task data, prepared unit solutions, reference answers, model weights, API keys or Team Key.

The agent inspects each task's instruction, card, visible checker source and data-file previews at runtime. It first asks the approved House model to identify the mathematics and output contract, then requests a complete program. It executes that program, runs visible checks in an isolated scratch directory, sends failures back for repair and preserves the best small output tree. The preview checks do not replace the organizer's verifier or establish an official score.

## Verified locally

- Eleven synthetic harness tests passed on Python 3.13, covering repair and best-candidate recovery, timeout handling, secret/canary protection, stale reports, archive inspection and the House request contract. Two additional spreadsheet/Parquet schema tests require image dependencies and are pending Linux verification.
- Task-context inspection succeeded on all 86 public units at official commit `3fa6e295601b18e0427502117a26ac4fcf32cdb2`; source files were unchanged. See `practice-audit.json`. This is an inspection audit, **not 86 solved tasks**.
- Linux Docker compatibility, dependency installation and real House-model execution still require testing.

## Budgets and reproducibility

Reads the card's agent timeout; caps work at 420 seconds per unit to limit total-roster exhaustion. The eight repair attempts plus one planning request are below the 25-request maximum, and every request caps output at 4,000 tokens. Admitted failures are counted conservatively. Uses fixed temperature 0 and the injected `QFBENCH_SEED`; disables default thinking to reserve output space for executable code. Neither this setting nor the budget is yet optimized on official evaluations.

The generated program receives no model credential or proxy credentials. The supervisor alone calls the approved House endpoint. The image contains only our general agent code and pinned libraries. All task inspection happens after the organizer mounts the new unit.

Binary inputs receive runtime schema inspection: spreadsheet sheet names/first rows, Parquet columns/row counts, and archive member names/sizes without extraction. No prepared per-unit solution is included.

## Research and design rationale

1. [Official Track 1 kit](https://github.com/Agenthon-2026/track1-coding-public), pinned to the commit above: runtime House use is mandatory, same-unit stored solutions are prohibited, paths and output formats vary, and the total-roster clock matters. There is no official baseline agent. Track 1 permits one Development upload per day, 23 total.
2. [SWE-agent](https://arxiv.org/abs/2405.15793): motivates a controlled interface for repository inspection, editing and execution feedback. We use bounded Python execution rather than an unrestricted shell.
3. [Agentless](https://arxiv.org/abs/2407.01489): motivates a focused inspection/generation/validation loop instead of a large orchestration framework. Its software-repair benchmark results do not predict Agenthon performance.
4. [Reflexion](https://arxiv.org/abs/2303.11366): motivates feeding concrete failures back into subsequent attempts. We retain per-task feedback only and do not learn from sealed outputs.
5. [Official House guide](https://github.com/Agenthon-2026/Agenthon2026-public/blob/v2.5.1/docs/HOUSE-MODEL.md): origin plus `/v1/chat/completions`, runtime alias/token, exact disclosure and supported thinking control.

Targeted searches did not identify a verified public implementation of the current leading Track 1 teams. A leaderboard number alone does not reveal an approach.

## Next evaluation

Build Linux/amd64, test non-root/read-only/noexec-tmp behavior, publish and verify an anonymous pull by immutable digest. Then create a descriptor and team proof with toolkit v2.5.1. Use one Development evaluation to measure genuine House performance and inspect failure classes before changing the method.

Known limits: 4,000-token complete-program responses may constrain complex tasks; relative checker paths and missing reference files may make a preview inconclusive; the 420-second budget trades depth against roster coverage. Dependency pins and actual House latency need cloud verification. No top-three or 80% result is claimed.
