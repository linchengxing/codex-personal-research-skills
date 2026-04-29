# Output Templates

Use these only when you need a compact answer skeleton.

## Blocked

```markdown
Blocked by underspecified implementation details.

Need user confirmation on:
- ...
- ...

Plausible branches:
- A: ...
- B: ...

Do not continue to implementation until these are answered.
```

## Proceed

```markdown
Core entry points
- `path/to/train.py`: why it matters

Shortest path
- `train.py -> builder.py -> model.py -> forward`

Must change
- `path/to/file.py`: reason

Should not change
- `path/to/file.py`: reason

New file?
- no

Insertion point
- class or function and file

Main logic home
- file that should hold the mechanism

Thin wiring edits
- builder, config, or one loop hook only where needed

Data path impact
- what tensor or state changes

Fastest honest verification
- one forward pass, one short run, or one eval slice
```
