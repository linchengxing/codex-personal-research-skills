---
name: minimal-change-mapping
description: Use when a research repo is understood well enough to plan edits and the task is to identify the smallest viable set of files to change without spreading the method across the codebase.
---

# Minimal Change Mapping

## Overview

Use this after the repo is understood well enough to decide where the method should live. The job here is to shrink the change surface until it is just large enough to work.

REQUIRED BACKGROUND: follow `$research-repo-style` and preferably `$repo-reading-for-research` first.

## Workflow

1. Restate the user's mechanism in one sentence.
2. List the files that must change for the method to exist.
3. List the files that are tempting but should stay untouched.
4. Decide whether a new file is truly justified.
5. If the file map depends on an unspecified idea detail, pause and ask the user before fixing the plan.
6. Explain why this file set is the smallest viable closed loop.

## Output Contract

Always return:

- `Target mechanism`
- `Must change`
- `Should not change`
- `New file?`
- `Why this is minimal`

Each file should have a one-line reason. If a new file is justified, say what single concept it owns.

## Guardrails

- Default to editing existing files.
- A new file must correspond to one clear concept, not general plumbing.
- Reject changes that move core logic farther away from the main path.
- Avoid vague advice such as "touch the model and training code." Name the likely files.
- If multiple file maps are plausible because the idea is underspecified, do not choose one silently. Ask the user.
