# Research Module Implementation Design

Date: 2026-04-29
Topic: research-module-implementation
Status: Approved design written from brainstorming

## 1. Purpose

Refactor this repository from a multi-skill research coding suite into a single-skill repository centered on one public skill:

- `research-module-implementation`

This skill should support one high-frequency workflow:

- read an existing deep learning research repo
- identify the shortest viable implementation path
- minimize the change surface
- implement one research module or mechanism with minimal intrusion
- stop and ask the user whenever unresolved details would affect implementation direction

## 2. Scope

This skill is domain-agnostic.

It must not be framed as specific to:

- MLLM
- 3D point cloud understanding
- embodied AI
- any other named research subfield

Instead, it should be framed around a generic deep learning research codebase.

## 3. Repository Goal

The repository should expose only one public skill.

After the redesign, the repository should no longer present itself as a skill suite. It should present itself as one focused skill for implementing research mechanisms inside existing deep learning repos.

## 4. Core Problem Being Solved

The user's actual usage pattern is concentrated on the current `surgical-module-insertion` flow, not on the broader multi-skill setup.

The current structure has two problems:

1. too many visible skills for the real usage frequency
2. insufficiently strict questioning before implementation when important details are missing

The redesign must solve both:

- reduce the public interface to one skill
- strengthen the requirement to ask the user before committing to implementation branches

## 5. New Public Skill

The single public skill should be named:

- `research-module-implementation`

This replaces the public role previously split across:

- `research-repo-style`
- `repo-reading-for-research`
- `minimal-change-mapping`
- `surgical-module-insertion`

## 6. Responsibilities

`research-module-implementation` should absorb these four capabilities:

### 6.1 Repo reading

It should read an unfamiliar deep learning research repo from the perspective of the requested mechanism, not from the perspective of exhaustive repo summarization.

### 6.2 Change-surface reduction

It should identify the smallest viable set of files to touch before implementation starts.

### 6.3 Minimal-intrusive mechanism implementation

It should guide implementation toward local, repo-native edits rather than abstractions or framework-like layers.

### 6.4 Hard-stop confirmation

If the method, repo path, implementation boundary, or code structure still depends on unresolved details, the skill must stop and ask the user before coding further.

## 7. Explicit Non-Responsibilities

The single skill should not expand into a full research lifecycle tool.

It should not directly own:

- full eval or ablation planning
- code review workflow
- general debugging workflow
- brainstorming
- paper writing

Those are outside the intended high-frequency use case.

## 8. Internal Stages

Although the repository exposes only one skill, that skill should internally operate in four stages:

1. `Repo Read`
2. `Change Surface`
3. `Implementation Gate`
4. `Module Implementation`

These stages should be documented inside one `SKILL.md`, not split into separate public skills.

## 9. Stage Details

### 9.1 Repo Read

The skill should:

- start from the requested mechanism or behavior change
- identify entry scripts, model builders, forward paths, and relevant train/infer cut points
- stop once the likely edit path is clear

It should avoid broad repo tours.

### 9.2 Change Surface

The skill should:

- name the files that must change
- name the files that should preferably stay untouched
- decide whether a new file is actually justified
- explain why the resulting file set is the smallest viable closed loop

### 9.3 Implementation Gate

This is the most important stage.

Before implementation, the skill must decide whether the next concrete action can be chosen without inventing important assumptions.

If not, it must ask the user.

### 9.4 Module Implementation

If the task is sufficiently specified, the skill should:

- choose one obvious home for the main logic
- keep surrounding edits thin
- prefer existing repo style over new abstractions
- verify with the lightest honest check

## 10. Hard-Stop Confirmation Policy

The skill must ask the user before proceeding whenever unresolved details would materially affect:

- module structure
- insertion point
- data flow
- routing or scoring logic
- training versus inference behavior
- file layout
- implementation boundary

Examples include:

- original-file edit vs new file split
- whether a module should be inserted before or after an existing stage
- whether two branches share a mask or use separate policies
- what exact budget, gating, or routing rule to implement first
- whether the first version is only a minimal running version or also includes extra integration

## 11. Conservative Questioning Rule

The user asked for a stronger questioning policy than the current implementation provides.

Therefore the skill should follow this rule:

> If two or more plausible implementation branches exist, and choosing one would change code structure, behavior, or downstream interpretation, ask the user instead of deciding alone.

This rule is intentionally stricter than typical "reasonable assumption" behavior.

## 12. Domain-Neutral Framing

The skill text and README must avoid domain-specific positioning.

Allowed framing:

- deep learning research repo
- research module
- research mechanism
- model path
- training or inference logic

Avoid using specific topical framing as the core identity of the skill.

Specific domains may still appear in examples later if needed, but not in the skill's defining scope.

## 13. Output Format

The skill should support three primary response modes.

### 13.1 Blocked

When unresolved details prevent implementation:

```text
Blocked by underspecified implementation details.

Need user confirmation on:
- ...
- ...

Do not continue to implementation until these are answered.
```

### 13.2 Repo path not yet fixed

When repo reading is still the main task:

```text
Read first:
- ...
- ...

Likely edit files:
- ...
- ...

Need user confirmation on:
- ...
```

### 13.3 Sufficient to implement

When the next code step is clear:

```text
Implementation path:
- Main logic home: ...
- Thin wiring edits: ...
- Files to avoid touching: ...

Proceeding with minimal-intrusive implementation.
```

## 14. Tone Constraints

The skill should be:

- direct
- compact
- explicit about uncertainty
- explicit about why a question is being asked
- free of generic software-architecture language unless the repo actually uses it

It should not rely on vague words such as:

- modular
- scalable
- extensible
- clean architecture

unless those claims are tied to concrete repo behavior.

## 15. Reference Strategy

Keep the repository public surface to one skill, but allow a small private support structure inside that skill:

- `references/repo-archetypes.md`
- `references/anti-patterns.md`
- `references/output-templates.md`

These references should be domain-neutral and only support this one skill.

## 16. Files To Remove

The redesign should remove these public skill directories from the repository:

- `using-research-skills/`
- `research-repo-style/`
- `repo-reading-for-research/`
- `minimal-change-mapping/`
- `surgical-module-insertion/`
- `training-loop-intervention/`
- `eval-ablation-extension/`
- `research-code-review/`

They should not remain as public install targets.

## 17. Final Repository Layout

After implementation, the intended top-level layout is:

- `research-module-implementation/`
- `README.md`

Inside the skill directory:

- `research-module-implementation/SKILL.md`
- `research-module-implementation/agents/openai.yaml`
- `research-module-implementation/references/repo-archetypes.md`
- `research-module-implementation/references/anti-patterns.md`
- `research-module-implementation/references/output-templates.md`

## 18. Description Requirement

The final skill description should describe when to use the skill, not how it works.

It should communicate:

- existing deep learning research repo
- implementing a new module or mechanism
- reading the repo first
- minimizing the change surface
- confirming missing implementation details before coding

It should not summarize a multi-step workflow in detail.

## 19. README Direction

README should be rewritten to reflect a single-skill repository.

It should:

1. present only `research-module-implementation`
2. describe the absorbed capabilities:
   - repo reading
   - change-surface reduction
   - minimal-intrusive implementation
   - hard-stop user confirmation
3. explain that this skill does not cover full eval/review/debugging workflows
4. update all install and update instructions to reference only one skill

## 20. Acceptance Criteria

The redesign is successful if:

1. only one public skill remains
2. the new skill is domain-neutral
3. it absorbs the useful behavior previously spread across four skills
4. it asks the user more aggressively before unresolved implementation choices
5. it remains focused on repo reading, change-surface reduction, and mechanism implementation
6. it does not expand into eval/review/full-lifecycle scope

## 21. Implementation Notes

Implementation should prefer consolidation over indirection.

The main `SKILL.md` should be strong enough to work on its own.

References should remain short and only exist to keep the main skill readable, not to recreate a hidden multi-skill framework.
