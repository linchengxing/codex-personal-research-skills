# Implementation Plan

Date: 2026-04-29
Spec: [2026-04-29-research-module-implementation-design.md](../specs/2026-04-29-research-module-implementation-design.md)

## Goal

Refactor the repository from a multi-skill suite into a single public skill named `research-module-implementation`, while preserving the useful behavior of repo reading, minimal change mapping, paper-repo style preservation, and surgical module insertion.

## Steps

1. Create the new public skill directory.
2. Fold gate, repo-reading, change-surface, and module-insertion behavior into one `SKILL.md`.
3. Add minimal shared references required by the new skill.
4. Rewrite `README.md` around a single-skill install and usage flow.
5. Remove the old public skill directories from the repository.
6. Validate structure, placeholders, and install-facing metadata.
7. Commit and push the refactor.
