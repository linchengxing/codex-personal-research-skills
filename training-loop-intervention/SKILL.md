---
name: training-loop-intervention
description: Use when modifying train or eval loop behavior in a research repo, such as losses, sampling, token budgets, or distillation, without adding new framework layers.
---

# Training Loop Intervention

## Overview

Use this when the research change lives in the training or evaluation behavior rather than in a new structural module. The goal is to patch the existing loop, not replace it.

REQUIRED BACKGROUND: follow `$research-repo-style` and `$minimal-change-mapping` first.

## Workflow

1. Find the current loop cut point: batch prep, forward call, loss construction, post-processing, cache update, or metric logging.
2. Insert the new behavior at the narrowest point that changes the result.
3. Keep new state small and local.
4. Reuse the repo's current logging and argument plumbing.
5. If the loop change depends on an unspecified policy or objective, ask the user before implementing.
6. Verify with a single-batch or very short run before scaling up.

## Output Contract

Always return:

- `Loop cut point`
- `Minimal edit plan`
- `New state or signals`
- `Likely side effects`
- `Shortest verification`

## Good Targets

- new loss terms
- sampling policies
- token budgets
- distillation hooks
- cache or memory behavior
- train-time gating decisions

## Guardrails

- Prefer patching the existing loop over creating a new trainer.
- Do not add framework-style callback systems unless the repo already depends on them.
- Keep loop changes readable in the main train path.
- Be explicit about side effects on metrics, speed, and memory.
- Do not assume missing details such as loss form, schedule, sampling rule, gating logic, or logging behavior. Ask the user first.
