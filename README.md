# Research Module Implementation for Codex

这个仓库现在只暴露一个公开 skill：

- `research-module-implementation`

它面向通用 deep learning research coding，不绑定任何具体研究方向。

目标很明确：

- 先读 repo，再决定改哪里
- 把改动面压到最小
- 保持代码像论文 repo，而不是被工程化改造
- 只要有任何会影响实现方向的细节没写清，就先问用户，再继续实现

## Public Skill

### `research-module-implementation`

这个 skill 把原来几类最常用能力合并成一个内部流程：

1. 读 repo，找最短调用路径
2. 缩改动面，明确哪些文件必须改、哪些不要碰
3. 做实现前门禁，检查是否有关键细节缺失
4. 在最小改动下把一个研究模块或机制接进现有代码路径

它适合的任务包括：

- 往现有模型里插一个模块
- 增加 router、selector、adapter、head、memory block
- 在不重构 repo 的前提下实现一个新机制
- 根据 `idea.md` 或方法描述落地 v1 代码

它不做的事情：

- 全套 ablation / eval 平台化
- 通用 code review 流程
- 脱离实现任务的 brainstorming

## Behavior Guarantee

这个 skill 明确要求：

- 不默认新建 `utils.py`、`helpers.py`、`manager.py`、`wrapper.py`
- 不为了“更优雅”把核心逻辑拆成很多层
- 不做与当前研究改动无关的重构
- 不假设具体应用领域
- 不自动补全 idea 里没写清的关键方法细节

下面这条是硬约束，不是建议：

如果有任何不确定内容会影响实现方向，Codex 必须先问你，不能自己补。

典型会触发停下确认的情况包括：

- 模块插入点不明确
- 路由或打分规则没定义
- 训练时和推理时是否一致不明确
- shared branch 还是 separate branch 不明确
- 改旧文件还是拆新文件会明显改变实现结构

如果存在两个以上合理实现分支，也必须先把分支列出来问你，不能静默拍板。

## Install

Codex 的个人 skills 默认放在：

```bash
~/.codex/skills
```

### Conversational Install via Codex

如果目标机器上的 Codex 带有系统 skill `$skill-installer`，直接说：

```text
Use $skill-installer to install research-module-implementation from linchengxing/codex-personal-research-skills.
```

安装完成后，建议重启 Codex，让新 skill 被重新发现。

### Copy Into Codex

如果你是手动同步，在仓库根目录执行：

```bash
mkdir -p ~/.codex/skills

rsync -a \
  research-module-implementation \
  ~/.codex/skills/
```

### Direct Installer Script

如果你想手动调用系统安装脚本：

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo linchengxing/codex-personal-research-skills \
  --path research-module-implementation
```

## Update

### Option 1: Reinstall via `skill-installer`

```text
Use $skill-installer to install research-module-implementation from linchengxing/codex-personal-research-skills.
```

### Option 2: Pull and Sync

```bash
git pull

rsync -a \
  research-module-implementation \
  ~/.codex/skills/
```

### If You Installed the Old Multi-Skill Version

旧版本如果装过这些目录，建议先删掉：

```bash
rm -rf ~/.codex/skills/using-research-skills
rm -rf ~/.codex/skills/research-repo-style
rm -rf ~/.codex/skills/repo-reading-for-research
rm -rf ~/.codex/skills/minimal-change-mapping
rm -rf ~/.codex/skills/surgical-module-insertion
rm -rf ~/.codex/skills/training-loop-intervention
rm -rf ~/.codex/skills/eval-ablation-extension
rm -rf ~/.codex/skills/research-code-review
```

然后安装新的单 skill 版本。

## How To Use

最稳妥的方式是显式调用：

```text
Use $research-module-implementation to read this repo, find the smallest valid edit surface, and implement this module. If any missing detail would affect the implementation, ask me before coding.
```

如果你已经有 `idea.md`，可以直接这样说：

```text
Read my idea.md first. Use $research-module-implementation to turn it into a v1 implementation path and code it in this repo. If any detail is underspecified and changes the implementation direction, stop and ask me before coding.
```

如果你想强调不要工程化，可以这样说：

```text
Use $research-module-implementation to add this mechanism, keep the repo style intact, keep the change surface small, and do not introduce wrappers or helper layers. Ask me before deciding any unspecified detail.
```

## Install-Facing Layout

对安装真正重要的是下面这部分：

```text
research-module-implementation/
README.md
```

其中：

- `research-module-implementation/SKILL.md` 是核心行为定义
- `research-module-implementation/agents/openai.yaml` 是 Codex metadata
- `research-module-implementation/references/` 放最小必要参考材料

## Local Source Note

如果你在本机开发和测试，这个 skill 的安装目标仍然是：

```bash
~/.codex/skills
```
