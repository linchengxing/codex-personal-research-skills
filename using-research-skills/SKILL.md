---
name: using-research-skills
description: Use when the user explicitly wants one entry point for this repo's research skills, and the task should first check for underspecified implementation details before routing to the right downstream skill.
---

# Using Research Skills

## Overview

Use this as the explicit entry point for this repository's research skills. It does two things in order:

1. gate on underspecified implementation details
2. route to the minimum necessary downstream research skill set

This skill is explicit-only. Do not assume it governs all conversations by default.

## Gate First

Before routing, decide whether the next concrete action can be chosen without inventing important assumptions.

If unresolved details would materially affect implementation direction, stop and ask the user before continuing.

Hard-stop uncertainty classes include:

- method structure
- data flow
- training or inference behavior
- evaluation scope
- implementation boundary

Examples:

- module insertion point is unclear
- shared mask vs separate masks is unclear
- training-free vs trainable behavior is unclear
- benchmark or ablation scope is unclear
- original-file edit vs new-file split would materially shape the implementation

Do not treat "good enough to start" as permission to fill in missing method details.

## Routing Rules

If the task is sufficiently specified, always include:

- `$research-repo-style`

Then route by dominant intent:

- understand an unfamiliar repo
  - `$repo-reading-for-research`
- shrink the edit surface before coding
  - `$minimal-change-mapping`
- insert one research mechanism into the model path
  - `$surgical-module-insertion`
- modify train or eval loop behavior
  - `$training-loop-intervention`
- add benchmarks, evals, or ablations
  - `$eval-ablation-extension`
- review diffs for correctness or style drift
  - `$research-code-review`

## Invocation Policy

Default behavior:

- invoke the matching downstream research skill

Exception:

- if the request is only a narrow explanatory question and not yet an action request, suggestion is allowed instead of mandatory invocation

Do not invoke many downstream skills reflexively. Preferred pattern:

- `$research-repo-style`
- one primary downstream skill

Add a second downstream skill only when the task clearly spans two adjacent phases.

Do not route into skills outside this repository.

## Output Format

If blocked, answer in this shape:

```text
Blocked by underspecified implementation details.

Need user confirmation on:
- ...
- ...

Do not continue to implementation or deeper routing until these are answered.
```

If sufficient, answer in this shape:

```text
Sufficient to proceed.

Invoke:
- $research-repo-style
- $minimal-change-mapping

Reason:
- ...
```

## Constraints

- be direct
- be strict about missing details
- be minimal in wording
- explain why the routing happened

This skill is not a replacement for the downstream skills. It is only the gate and router.
