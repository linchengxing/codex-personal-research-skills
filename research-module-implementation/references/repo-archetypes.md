# Repo Archetypes

Use this file only when the repo shape is unclear.

## 1. Plain Paper Repo

Typical signs:

- `train.py`, `eval.py`, `run.sh`
- one or two large model files
- direct argument parsing
- minimal abstraction

How to work:

- read the entry scripts first
- trace the model constructor and forward path
- keep edits local even if the file is large

Do not fight:

- manual arguments
- direct imports
- script-heavy workflows

## 2. HF-Style Repo

Typical signs:

- `modeling_*.py`
- `configuration_*.py`
- `train*.py`
- `transformers`, `accelerate`, or similar libraries

How to work:

- find the real forward path before touching config
- keep new logic near the model path, not in launch code
- keep config exposure minimal

Do not fight:

- existing config classes
- the repo's current builder style
- launch scripts that already work

## 3. Registry-Heavy Repo

Typical signs:

- registries
- config trees
- builders
- modular components spread across folders

How to work:

- respect the existing registration path
- still keep the new idea concentrated in one obvious module
- touch registry or config wiring only as much as needed

Do not fight:

- the registry itself
- the config entry pattern

## 4. Hybrid or Custom-Op Repo

Typical signs:

- preprocessing scripts
- custom CUDA ops or compiled extensions
- separate train and eval stacks
- brittle environment setup

How to work:

- identify whether the real bottleneck is model code, data prep, or the outer loop
- avoid touching expensive or brittle subsystems unless the method truly depends on them
- verify with the cheapest honest run because full loops may be expensive

Do not fight:

- unrelated custom ops
- unrelated environment setup
