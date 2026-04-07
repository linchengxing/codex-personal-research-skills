---
name: research-code-review
description: Use when reviewing changes to a research repo and you need to catch bugs, style drift, over-abstraction, or logic spread that makes the code feel less like a paper repo.
---

# Research Code Review

## Overview

Use this to review research code with two goals at once: catch real bugs or regressions, and catch style drift that makes the repo less readable, less local, or less like the original paper code.

REQUIRED BACKGROUND: follow `$research-repo-style` first. If needed, read `../research-repo-style/references/anti-patterns.md`.

## Review Order

1. Find correctness risks first: bugs, behavioral regressions, broken assumptions, missing wiring, missing verification.
2. Then look for style drift: unnecessary abstraction, logic split across too many files, new layers that hide the method, or edits that fight the repo's existing conventions.
3. Prefer actionable findings over general advice.

## Output Contract

Present findings first, ordered by severity. For each finding include:

- file reference
- what changed or is risky
- why it harms correctness or paper-repo readability
- the lighter alternative when one exists

After findings, include only brief open questions or residual risks.

## Things To Flag Aggressively

- one mechanism spread across too many files
- new wrappers, managers, or registries that were not needed
- core logic moved out of the main path into vague helpers
- reviews that praise "clean architecture" while making the method harder to follow
- missing smoke checks for a meaningful behavior change

## If No Findings

Say so explicitly. Then mention any remaining verification gaps without inventing stylistic complaints.
