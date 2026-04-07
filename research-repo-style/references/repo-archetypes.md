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

## 2. HF or MLLM Repo

Typical signs:

- `modeling_*.py`
- `configuration_*.py`
- `train*.py`
- `transformers`, `accelerate`, or `deepspeed`

How to work:

- find the actual forward path before touching config
- keep new method logic near the model path, not in launch code
- keep config exposure minimal

Do not fight:

- existing config classes
- the repo's current builder style
- launch scripts that already work

## 3. MM-Style or Registry-Heavy Repo

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

## 4. 3D or Embodied Hybrid Repo

Typical signs:

- data preprocessing scripts
- simulator or environment wrappers
- CUDA ops or custom extensions
- separate train and eval stacks

How to work:

- identify whether the real bottleneck is model code, data prep, or environment rollout
- avoid touching environment or preprocessing code unless the method truly depends on it
- verify with the cheapest honest run because full loops may be expensive

Do not fight:

- brittle environment setup
- custom ops that are unrelated to the method change
