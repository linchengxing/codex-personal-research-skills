---
name: research-module-implementation
description: Use when implementing one deep learning research mechanism in an existing repo and the goal is to read the repo first, keep the change surface small, preserve paper-repo style, and stop to ask the user whenever any missing detail would affect implementation. 适用于“先读 repo 再改”“最小改动插入模块”“不要工程化”“细节不清先问我”。
---

# Research Module Implementation

## Overview

Use this when the task is to implement one research mechanism inside an existing deep learning repo without turning the repo into a framework.

This skill combines four internal stages:

1. repo read
2. change surface
3. implementation gate
4. module implementation

The goal is simple:

- find the shortest path to the real edit point
- keep the file set small
- keep the main logic locally visible
- stop and ask the user whenever missing details would change the implementation

## Stage 1: Repo Read

Start from the user's requested mechanism, not from the full directory tree.

Find only the shortest path that matters:

- entry script
- model builder
- forward path
- train or eval path only if it directly affects the mechanism

Stop reading once the likely edit surface is clear.

## Stage 2: Change Surface

Before coding, shrink the change set to the smallest viable closed loop.

Always identify:

- the files that must change
- the files that should stay untouched
- whether a new file is truly justified

Default to editing existing files. If a new file is needed, it should own one clear concept such as a selector, router, adapter, head, or loss.

## Stage 3: Implementation Gate

Before implementing, check whether any unresolved detail would materially affect code structure, behavior, or the interpretation of the method.

Hard-stop uncertainty classes include:

- module structure
- insertion point
- tensor or state flow
- shared versus separate branches
- routing or scoring rule
- trainable versus fixed behavior
- training-only versus inference-time behavior
- budget, masking, caching, or update rule
- existing-file edit versus new-file split
- any other choice that changes the implementation path

If any such detail is missing, stop and ask the user before coding.

If there are two or more plausible implementation branches, do not choose one silently. Present the branches briefly and ask the user which direction to take.

Do not treat "good enough to start" as permission to invent method details.

## Stage 4: Module Implementation

Once the task is sufficiently specified:

1. choose one obvious home for the main mechanism
2. keep surrounding edits thin
3. preserve the repo's current naming, argument, config, and construction style
4. keep the core logic visible in one obvious place
5. verify with the lightest honest check that proves the mechanism is wired correctly

Typical thin wiring edits are:

- builder exposure
- config or argument exposure
- one forward-path call
- one train or eval hook if the method truly needs it

## Output Contract

If blocked by missing details, answer in this shape:

```text
Blocked by underspecified implementation details.

Need user confirmation on:
- ...
- ...

Plausible branches:
- A: ...
- B: ...

Do not continue to implementation until these are answered.
```

If sufficiently specified, answer in this shape:

```text
Core entry points
- `path/to/file.py`: why it matters

Shortest path
- `train.py -> builder.py -> model.py -> forward`

Must change
- `path/to/file.py`: reason

Should not change
- `path/to/file.py`: reason

New file?
- no

Insertion point
- class or function and file

Main logic home
- file that should hold the mechanism

Thin wiring edits
- builder or config exposure only where needed

Data path impact
- what tensor or state now flows through the new step

Fastest honest verification
- one forward pass, one short run, or one eval slice
```

## Guardrails

- Do not create `utils.py`, `helpers.py`, `manager.py`, or `wrapper.py` by default.
- Do not spread one mechanism across a long helper chain.
- Do not introduce a new registry, trainer wrapper, service layer, or framework abstraction unless the repo already depends on that pattern.
- Do not do unrelated cleanup refactors.
- Do not move core logic farther away from the main model or loop path just to make the code look more abstract.
- Do not silently fill in idea details that the user did not specify.
- Do not assume any specific application domain. Work from the repo and the user's method description only.

## References

- `references/repo-archetypes.md` for common repo shapes
- `references/anti-patterns.md` for over-engineering smells
- `references/output-templates.md` for compact output skeletons
