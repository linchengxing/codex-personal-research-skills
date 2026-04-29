# Anti-Patterns

Use this file when a proposed change starts feeling too engineered.

## 1. One Method, Five Files

Smell:
The new idea only works after touching builders, wrappers, helpers, registries, and service layers.

Lighter move:
Ask whether the main mechanism can live in one existing model or loop file, with only thin wiring elsewhere.

## 2. New Generic Helpers

Smell:
The core logic gets hidden inside `utils.py`, `helpers.py`, or `common.py`.

Lighter move:
Keep the method where the reader expects to find it. Helpers should only hold boring, repeated glue.

## 3. Wrapper Around The Whole Model

Smell:
One new mechanism causes a new outer model class or manager even though the repo did not need one before.

Lighter move:
Patch the existing construction and forward path unless there is a real need for a new top-level object.

## 4. Refactor Disguised As Research

Smell:
"I needed to clean up the repo first" expands the change set far beyond the experiment.

Lighter move:
Refactor only the local section that blocks the method.

## 5. Pretty But Harder To Read

Smell:
The diff looks more elegant to engineers but makes the research contribution harder to find.

Lighter move:
Prefer local visibility over abstraction purity.

## 6. Silent Method Completion

Smell:
The code quietly picks a routing rule, mask policy, branch split, or training behavior that the idea never specified.

Lighter move:
Stop and ask the user before fixing the design in code.
