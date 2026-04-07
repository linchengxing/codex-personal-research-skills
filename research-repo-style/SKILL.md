---
name: research-repo-style
description: Use when reading, modifying, or reviewing an existing research repo and the task should preserve the repo's original paper-style structure instead of engineering it into a framework.
---

# Research Repo Style

## Overview

Use this as the style governor for research coding. The goal is to behave like the paper authors continuing the repo, not like an external engineer redesigning it.

## Core Rules

1. Preserve the repo. Do not "upgrade" it into a framework unless the repo already works that way.
2. Read first, cut second, write last. Find the shortest path to the method before proposing edits.
3. Prefer editing existing files over adding wrappers, managers, helpers, or new orchestration layers.
4. Keep core research logic locally visible. A reader should see the main mechanism in one obvious place.
5. One new concept, one obvious home. If a new file is unavoidable, it should hold one clear thing such as a selector, router, loss, or head.
6. No unrelated cleanup refactors. Only refactor when the current structure blocks the experiment.
7. Follow local style over abstract best practice. Reuse the repo's naming, argument style, config style, and script conventions.
8. Verify lightly but honestly. Prefer smoke checks, shape checks, short runs, and minimal evals over product-grade test harnesses.
9. If the idea or repo leaves any material implementation detail unspecified, stop and ask the user before continuing. Do not silently invent method details that affect behavior, claims, data flow, training dynamics, or evaluation scope.

## Default Workflow

1. Identify the repo archetype. If unsure, read `references/repo-archetypes.md`.
2. Trace the shortest working path from entry point to the user's intended change.
3. State the likely edit files before writing code.
4. State what should stay untouched.
5. If a required implementation choice is still uncertain, ask the user before writing code.
6. Implement the smallest closed loop that proves the method.

## Hard Red Flags

- adding `utils.py`, `helpers.py`, `manager.py`, or `wrapper.py` by default
- spreading one research idea across a long call chain
- introducing a new registry, config system, trainer wrapper, or service layer without a repo-native reason
- replacing a readable in-place edit with a more abstract but less obvious design
- silently filling in idea details the user did not specify
- turning eval or ablation work into a new platform
- doing "while we're here" cleanup unrelated to the user's experiment

## Response Style

- Lead with the actionable conclusion.
- Use real repo file names, class names, and scripts whenever possible.
- Prefer "edit these 3 files" over long repo tours.
- Push back directly when a proposed change would make the repo less like a paper repo.

## References

- `references/repo-archetypes.md` for common research repo shapes
- `references/anti-patterns.md` for smells and lighter alternatives
- `references/output-templates.md` for compact output skeletons
