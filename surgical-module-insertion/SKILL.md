---
name: surgical-module-insertion
description: Use when inserting one research mechanism into an existing model path and the goal is to keep most of the original repo intact.
---

# Surgical Module Insertion

## Overview

Use this when the task is to add one research mechanism, such as token pruning, routing, a small memory unit, an adapter, or a head, without turning the repo into a new system.

REQUIRED BACKGROUND: follow `$research-repo-style` and `$minimal-change-mapping` first.

## Workflow

1. Locate the exact attach point in the current model path.
2. Choose one obvious home for the new mechanism.
3. Keep surrounding edits thin: builder wiring, config exposure, and forward-path calls only where needed.
4. Prefer the repo's current argument and construction style over introducing a new pattern.
5. If insertion depends on an unspecified design choice, ask the user before implementing.
6. Verify with the lightest check that proves the module is wired correctly.

## Output Contract

Always return:

- `Insertion point`
- `Main logic home`
- `Thin wiring edits`
- `Data path impact`
- `Fastest honest verification`

## Good Targets

- token pruning or token selection
- query-conditioned routing
- adapters
- small heads
- memory blocks
- lightweight selectors

## Guardrails

- Do not create a wrapper around the whole model unless the repo already uses wrappers.
- Do not split the mechanism across many helper files.
- Do not hide the important math or routing logic in utility modules.
- Keep configuration edits minimal and repo-native.
- Do not invent missing method details such as routing policy, selector target, branch location, or budget rule without user confirmation.
