---
name: eval-ablation-extension
description: Use when adding evaluations, ablations, or paper-style experiment scripts to an existing research repo without building a new experiment platform.
---

# Eval Ablation Extension

## Overview

Use this when the repo already runs and the next job is to add evaluations, ablations, comparison scripts, or result export in a paper-repo style.

REQUIRED BACKGROUND: follow `$research-repo-style` first.

## Workflow

1. Reuse the repo's current eval and script layout before inventing a new one.
2. Add the smallest script or flag set that produces the needed result.
3. Keep outputs close to the current result organization.
4. Prefer direct scripts over generalized sweep infrastructure for v1.
5. If eval scope, metrics, or ablation axes are not stated in the idea, ask the user before adding them.
6. Make ablations claim-driven: only add the runs needed to support the paper story.

## Output Contract

Always return:

- `First eval pieces to add`
- `Recommended file or script locations`
- `What belongs in v1`
- `What can wait`
- `How results should be emitted`

## Preferred Forms

- `eval_*.py`
- `run_*.py`
- `scripts/*.sh`
- small argument additions to existing eval scripts
- direct result export compatible with current logs or tables

## Guardrails

- Do not build a platform just to run a few ablations.
- Do not create generic experiment managers by default.
- Keep filenames obvious and paper-oriented.
- Tie every new ablation back to a concrete claim or reviewer question.
- Do not infer extra benchmarks, metrics, or ablation axes from habit alone. Ask the user when the idea does not specify them.
