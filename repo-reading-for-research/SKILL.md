---
name: repo-reading-for-research
description: Use when a user wants to understand an unfamiliar research repo, find the shortest path to the edit point, or asks where to start reading before making a method change.
---

# Repo Reading for Research

## Overview

Use this to read a research repo with one question in mind: where is the shortest path from the user's requested method change to the actual code that matters?

REQUIRED BACKGROUND: follow `$research-repo-style` first.

## Workflow

1. Start from the user task, not from the full directory tree.
2. Find the real entry points: training script, evaluation script, model builder, dataset builder, forward path.
3. Walk the shortest path from entry point to the likely mechanism location.
4. Stop once the likely edit surface is clear. Do not summarize the entire repo.
5. If the repo shape is unusual, read `../research-repo-style/references/repo-archetypes.md`.
6. If multiple plausible edit paths exist and choosing one would change the implementation direction, stop and ask the user before proceeding.

## Output Contract

Always return:

- `Core entry points`: the first files or functions worth opening
- `Shortest path`: the smallest call path from entry script to method logic
- `Read first`: the 3-5 files worth reading in order
- `Likely edit files`: usually 2-4 files, with one-line reasons
- `Avoid for now`: files or subsystems that look adjacent but are probably not needed yet

## Guardrails

- Do not recommend refactors while reading.
- Do not reward large file counts. A shorter call path is better than a more "complete" tour.
- Prefer repo-local names over invented abstractions.
- If multiple plausible edit points exist, rank them instead of pretending there is only one.
- If the ranking depends on an idea detail the user never specified, ask instead of assuming.
