# Using Research Skills Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add `using-research-skills` as an explicit entry skill that performs a sufficiency gate before routing to the minimum necessary research skill(s).

**Architecture:** Add one new top-level skill directory with a concise `SKILL.md` and `agents/openai.yaml`, then update `README.md` so installation and usage treat it as the recommended entry point. Keep the new skill self-contained and avoid adding extra references unless they prove necessary later.

**Tech Stack:** Markdown, YAML frontmatter, Codex skill repo layout, git

---

### Task 1: Add the Entry Skill Directory

**Files:**
- Create: `using-research-skills/SKILL.md`
- Create: `using-research-skills/agents/openai.yaml`

- [ ] **Step 1: Write the new skill frontmatter**

```markdown
---
name: using-research-skills
description: Use when the user explicitly wants one entry point for this repo's research skills, and the task should first check for underspecified implementation details before routing to the right downstream skill.
---
```

- [ ] **Step 2: Write the body with gate-first behavior**

```markdown
# Using Research Skills

First perform a sufficiency check.
If material implementation details are unresolved, stop and ask the user.
Only after the task is sufficiently specified should the skill route to:
- $research-repo-style
- one primary downstream research skill
```

- [ ] **Step 3: Write the routing map and semi-hard invocation policy**

```markdown
Default:
- always include $research-repo-style
- invoke the matching downstream skill

Exception:
- if the user asks only a narrow explanatory question, suggestion is allowed instead of mandatory invocation
```

- [ ] **Step 4: Add Codex UI metadata**

```yaml
interface:
  display_name: "Using Research Skills"
  short_description: "Gate and route research coding tasks"
  default_prompt: "Use $using-research-skills to check whether a research coding task is specified enough and route it to the right skill."
```

### Task 2: Update the README

**Files:**
- Modify: `README.md`

- [ ] **Step 1: Add the new skill to the included skills list**

```markdown
### 1. `using-research-skills`

显式入口 skill。先检查信息是否足够，不足就先问用户；足够后再把任务路由到最合适的 research skill。
```

- [ ] **Step 2: Update install instructions to include the new skill**

```text
using-research-skills/
research-repo-style/
repo-reading-for-research/
minimal-change-mapping/
surgical-module-insertion/
training-loop-intervention/
eval-ablation-extension/
research-code-review/
README.md
```

- [ ] **Step 3: Update the recommended usage and workflow**

```text
Use $using-research-skills to gate and route this research coding task.
If any implementation detail is underspecified and would affect the direction, ask me before coding.
```

- [ ] **Step 4: State clearly that the entry skill does not replace the downstream skills**

```markdown
`using-research-skills` 不是替代其余 7 个 skills，而是负责先做门禁，再做最小必要分流。
```

### Task 3: Validate the Skill Structure

**Files:**
- Modify: `using-research-skills/SKILL.md`
- Modify: `README.md`

- [ ] **Step 1: Scan for placeholders**

Run: `rg -n "\\[TODO|TODO:" using-research-skills README.md`
Expected: no matches

- [ ] **Step 2: Run local structural validation**

Run:
`python3 - <<'PY'
import re
from pathlib import Path
skill = Path('using-research-skills')
text = (skill / 'SKILL.md').read_text()
assert re.match(r'^---\\n(.*?)\\n---\\n', text, re.DOTALL)
assert (skill / 'agents' / 'openai.yaml').exists()
assert 'TODO' not in text
print('OK using-research-skills')
PY`

Expected: `OK using-research-skills`

- [ ] **Step 3: Check git state**

Run: `git status --short`
Expected: only the new skill, README update, and the new plan file are modified or added

### Task 4: Commit the Implementation

**Files:**
- Modify: `using-research-skills/SKILL.md`
- Modify: `using-research-skills/agents/openai.yaml`
- Modify: `README.md`

- [ ] **Step 1: Stage the implementation**

```bash
git add using-research-skills README.md docs/superpowers/plans/2026-04-08-using-research-skills.md
```

- [ ] **Step 2: Commit**

```bash
git commit -m "feat: add using-research-skills entry skill"
```
