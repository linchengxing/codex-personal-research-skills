# Output Templates

Use these only when you need a compact answer skeleton.

## Repo Reading

```markdown
Core entry points
- `path/to/train.py`: why it matters

Shortest path
- `train.py -> builder.py -> modeling_x.py -> forward`

Read first
- `path/to/file1.py`
- `path/to/file2.py`

Likely edit files
- `path/to/file3.py`: why
- `path/to/file4.py`: why

Avoid for now
- `path/to/adjacent_area.py`: why not yet
```

## Minimal Change Mapping

```markdown
Target mechanism
- one sentence

Must change
- `path/to/file.py`: reason

Should not change
- `path/to/file.py`: reason

New file?
- no

Why this is minimal
- short explanation
```

## Surgical Module Insertion

```markdown
Insertion point
- class/function and file

Main logic home
- file that should hold the mechanism

Thin wiring edits
- builder or config exposure only where needed

Data path impact
- what tensor or state now flows through the new step

Fastest honest verification
- one forward pass, one short run, or one eval slice
```

## Research Code Review

```markdown
Findings
- `path/to/file.py`: risk and why it hurts correctness or paper-repo readability

Open questions
- only if needed

Residual risks
- only if needed
```
