# Using Research Skills Design

Date: 2026-04-08
Topic: using-research-skills
Status: Approved design written from brainstorming

## 1. Purpose

Add one explicit entry skill for the personal research skill suite:

- `using-research-skills`

This skill should provide one stable entry point similar in spirit to `using-superpowers`, but scoped only to this repo's research-coding skills.

Its job is:

1. perform a strict pre-implementation sufficiency check
2. route the task to the minimum necessary downstream research skill(s)

It should not become a broad global workflow framework.

## 2. Scope

The skill covers only the research skills in this repository:

- `research-repo-style`
- `repo-reading-for-research`
- `minimal-change-mapping`
- `surgical-module-insertion`
- `training-loop-intervention`
- `eval-ablation-extension`
- `research-code-review`

It does not manage external process skills such as brainstorming, planning, or debugging.

## 3. Trigger Model

This is an explicit entry skill.

It should trigger only when the user explicitly invokes:

- `$using-research-skills`

It should not attempt to implicitly govern every research conversation by default.

## 4. Core Role

`using-research-skills` is a combined:

- gatekeeper
- dispatcher

The gatekeeper role comes first.
The dispatcher role only runs after the task is judged sufficiently specified for the next step.

## 5. Primary Design Goal

The central design requirement is:

> If the idea, repo context, or task description leaves any material implementation detail unresolved, and that uncertainty could change implementation direction, the skill must stop and ask the user before further routing or implementation.

This is more important than speed.

## 6. Non-Goals

This skill should not:

1. automatically orchestrate the full lifecycle of every research task
2. invoke all downstream skills at once
3. silently fill in missing method details
4. replace the downstream skills' specialized instructions
5. become a second `using-superpowers`

## 7. Sufficiency Check

Before routing, the skill must decide whether the request is implementation-ready for the next step.

It should not ask whether the task is fully specified forever. It should ask whether the next concrete action can be chosen without inventing important assumptions.

### 7.1 Hard-stop uncertainty classes

The skill must stop and ask the user when uncertainty affects:

- method structure
  - where the mechanism is inserted
  - whether it is pre-fusion vs post-fusion
  - whether branches share masks or policies
- data flow
  - what tokens are affected
  - what signals are shared
  - what representation the method operates on
- training or inference behavior
  - training-free vs trainable
  - loss additions
  - schedules
  - selection or routing policies
- evaluation scope
  - benchmark choice
  - baseline set
  - required ablations
  - metrics that define success
- implementation boundary
  - whether new files are allowed
  - whether the fusion module may be changed
  - whether the task is only v1 wiring or includes scripts and experiments

### 7.2 Conservative confirmation rule

The user explicitly chose a high-confirmation mode.

Therefore, even when a decision is not absolutely central, if there are multiple plausible implementation branches and picking one would materially shape the code, the skill should ask instead of assuming.

Examples include:

- original-file edit vs new module file
- cosine similarity vs dot-product for a first relevance score
- which baseline repo or target model to implement first
- which ablations belong in v1

### 7.3 Anti-rationalization rule

The skill must not treat "good enough to start coding" as permission to invent missing details.

If the next action depends on a choice the user did not make, the skill should surface that choice explicitly.

## 8. Routing Rules

After the sufficiency check passes, route to the minimum necessary research skill set.

### 8.1 Always-on prelude

For any research coding task, first include:

- `research-repo-style`

### 8.2 Primary routing map

Route by dominant intent:

- understand an unfamiliar repo
  - `repo-reading-for-research`
- shrink the edit surface before coding
  - `minimal-change-mapping`
- insert one method or module into the model path
  - `surgical-module-insertion`
- modify train or eval loop behavior
  - `training-loop-intervention`
- add benchmarks, evals, or ablations
  - `eval-ablation-extension`
- review diffs for correctness and style drift
  - `research-code-review`

## 9. Hard vs Soft Invocation Policy

The user selected a semi-hard rule:

- default behavior: invoke the matching downstream skill
- exception: if the request is only a narrow explanatory question and not yet an action request, suggestion is allowed instead of mandatory invocation

Examples:

- "What does this skill do?" -> suggestion is enough
- "Which files should I edit?" -> must route
- "Implement this pruning module." -> must route

## 10. Minimal Context Rule

The skill should not invoke many downstream skills reflexively.

Preferred pattern:

- `research-repo-style`
- one primary downstream skill

Only add a second downstream skill when the task clearly spans two adjacent phases.

The point is to minimize context load and avoid recreating a process-heavy system.

## 11. Output Format

The output should be compact and decision-oriented.

### 11.1 If blocked

Use a structure like:

```text
Blocked by underspecified implementation details.

Need user confirmation on:
- ...
- ...

Do not continue to implementation or deeper routing until these are answered.
```

### 11.2 If sufficient

Use a structure like:

```text
Sufficient to proceed.

Invoke:
- $research-repo-style
- $minimal-change-mapping

Reason:
- ...
```

## 12. Tone and Response Constraints

The skill should be:

- direct
- strict about missing details
- minimal in wording
- explicit about why routing happened

It should not produce long essays or generic research advice.

## 13. Repository Layout

Add this as an eighth top-level skill:

- `using-research-skills/`

The repository will then contain:

- `using-research-skills/`
- `research-repo-style/`
- `repo-reading-for-research/`
- `minimal-change-mapping/`
- `surgical-module-insertion/`
- `training-loop-intervention/`
- `eval-ablation-extension/`
- `research-code-review/`

## 14. README Changes

After implementation, README should be updated to:

1. list `using-research-skills` first as the recommended entry point
2. explain that it does not replace the seven downstream skills
3. explain that it performs a hard-stop sufficiency check before routing

## 15. V1 Acceptance Criteria

The design is successful if the implemented skill does all of the following:

1. explicit invocation only
2. blocks on underspecified implementation details
3. asks the user before picking materially different implementation branches
4. always includes `research-repo-style` for research coding tasks
5. routes to the minimum necessary downstream skill set
6. avoids process sprawl and excessive context loading

## 16. Implementation Notes

Implementation should stay small.

This should be one skill directory with:

- `SKILL.md`
- `agents/openai.yaml`

No extra references are required unless repeated use later proves they are needed.
