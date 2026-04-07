# Personal Research Skills for Codex

一套面向 research coding 的个人 Codex skills，主要服务于以下场景：

- 修改已有论文 repo，而不是从零搭工程框架
- MLLM、3D point cloud、Embodied AI 等研究代码的快速读懂与最小侵入式改造
- 保持代码像论文仓库，而不是被“工程化重构”

这套 skills 的核心目标不是“把 repo 变得更现代”，而是让 Codex 更像一个懂 research repo 的合作者：

- 先读 repo，再决定改哪里
- 优先最小改动面
- 核心逻辑尽量集中在少数关键文件
- 少 wrapper、少 manager、少无意义跳转
- 遇到 idea 中没写清、但会影响实现方向的内容，必须先问用户，不能自己补设定

## Included Skills

### 1. `research-repo-style`

总风格约束 skill。任何 research coding 任务都建议先用它，确保后续实现不会滑向过度工程化。

### 2. `repo-reading-for-research`

用于快速读懂陌生 research repo，找出最短调用链、优先阅读文件和最可能的改动点。

### 3. `minimal-change-mapping`

用于在真正写代码前，把改动面收缩到最小闭环，明确：

- 哪些文件必须改
- 哪些文件尽量别碰
- 是否真的需要新文件

### 4. `surgical-module-insertion`

用于往现有模型路径中插入一个研究机制，例如：

- token pruning
- router
- adapter
- memory block
- lightweight head

### 5. `training-loop-intervention`

用于修改训练或评测流程中的研究逻辑，例如：

- loss
- sampling
- token budget
- distillation hook
- cache / memory behavior

### 6. `eval-ablation-extension`

用于补 benchmark、ablation、eval script、结果导出，保持论文 repo 常见的脚本风格。

### 7. `research-code-review`

用于 code review，重点检查：

- 真 bug / regression
- 逻辑是否被打散
- 是否引入了不必要的新抽象
- 是否破坏了原 repo 的论文味

## Design Principles

这套 skills 共享以下原则：

1. Preserve the repo, don't engineer it into a framework.
2. Read first, cut second, write last.
3. Prefer editing existing files over adding abstraction layers.
4. Keep core research logic locally visible.
5. If the idea is underspecified in a way that affects implementation, ask the user before continuing.

第 5 条非常重要：

如果 idea 里没有明确说明某个关键细节，而这个细节会影响实现方向、训练行为、数据流、loss、eval scope、ablation axis 或论文 claim，那么 Codex 必须停下来问你，而不是自己补全。

## Install

Codex 在这台机器上的个人 skills 默认放在：

```bash
~/.codex/skills
```

要在另一台机器安装这套 skills，只需要把对应 skill 目录复制进去。

### Recommended Repo Layout

推荐你把下面这些目录和本 README 一起放到 GitHub 仓库里：

```text
research-repo-style/
repo-reading-for-research/
minimal-change-mapping/
surgical-module-insertion/
training-loop-intervention/
eval-ablation-extension/
research-code-review/
README.md
```

### Copy Into Codex

如果这些 skill 目录和 `README.md` 在同一个仓库根目录下，可以在目标机器执行：

```bash
mkdir -p ~/.codex/skills

rsync -a \
  research-repo-style \
  repo-reading-for-research \
  minimal-change-mapping \
  surgical-module-insertion \
  training-loop-intervention \
  eval-ablation-extension \
  research-code-review \
  ~/.codex/skills/
```

如果你把这些 skill 放在仓库里的 `skills/` 子目录下，只需要把命令改成：

```bash
mkdir -p ~/.codex/skills

rsync -a \
  skills/research-repo-style \
  skills/repo-reading-for-research \
  skills/minimal-change-mapping \
  skills/surgical-module-insertion \
  skills/training-loop-intervention \
  skills/eval-ablation-extension \
  skills/research-code-review \
  ~/.codex/skills/
```

安装后建议新开一个 Codex 会话，让新 skill 的 metadata 被重新发现。

## How To Use

最稳妥的方式是显式调用 skill 名称，例如：

```text
Use $research-repo-style and $repo-reading-for-research to find the smallest edit path in this Video MLLM repo.
```

```text
Use $minimal-change-mapping and $surgical-module-insertion to add a query-aware token pruning module, but do not refactor the repo.
```

```text
Use $training-loop-intervention to modify the token budget logic in the current training loop. If any design detail is unclear, ask me before implementing.
```

```text
Use $eval-ablation-extension to add only the minimum ablations needed for the paper claim.
```

```text
Use $research-code-review to review whether this diff introduced over-abstraction or spread the logic too far.
```

## Recommended Workflow

对于大多数 repo 改造任务，推荐这样用：

1. `$research-repo-style`
2. `$repo-reading-for-research`
3. `$minimal-change-mapping`
4. 下面三者选一个：
   - `$surgical-module-insertion`
   - `$training-loop-intervention`
   - `$eval-ablation-extension`
5. `$research-code-review`

## Important Behavior Guarantee

这套 skills 明确要求：

- 不要默认新建 `utils.py` / `helpers.py` / `manager.py`
- 不要为了“优雅”把核心逻辑拆成很多层
- 不要顺手做与当前 research 改动无关的重构
- 不要自动补全 idea 里没有写明的关键方法细节
- 只要不确定内容会影响实现方向，就必须先和用户交流

如果你希望 Codex 更像“懂论文 repo 的研究搭子”，而不是“总想接管代码库的工程助手”，这套 skills 就是为这个目标设计的。

## Files That Matter

每个 skill 目录至少包含：

- `SKILL.md`
- `agents/openai.yaml`

其中：

- `SKILL.md` 是真正的 skill 内容
- `agents/openai.yaml` 是 Codex UI / metadata 兼容文件

`research-repo-style` 额外带了几个共享 reference：

- `references/repo-archetypes.md`
- `references/anti-patterns.md`
- `references/output-templates.md`

## Local Source Note

当前这套 skills 在本机的实际工作副本位于：

```bash
~/.codex/skills
```

如果你要把它们同步到 GitHub 并在其他机器复用，建议把上面列出的 7 个 skill 目录完整纳入仓库，然后按本 README 的安装方式同步到新的机器。
