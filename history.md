# History

## Summary

This repository started as a local clone of `garrytan/gstack`, but the intended usage was not web-product development. The goal was to adapt the gstack skill system and workflow discipline for CUDA/C++ numerical simulation work such as DEM, SPH, FVM, FEM, CFD, and related solver development.

## Phase 1: Initial Adaptation Direction

The original gstack repository was reviewed to determine which ideas transfer well to CUDA/C++ work.

### Kept from original gstack

These workflow ideas were considered broadly useful and retained conceptually:

- structured planning and review
- root-cause-first debugging
- explicit release gates
- safety controls such as `careful`, `freeze`, and `guard`
- engineering review style from `plan-eng-review`

### Considered web-specific or non-default for simulation work

These were identified as web-focused and not suitable as the default workflow for solver development:

- `browse`
- `qa`
- `qa-only`
- `design-review`
- `design-consultation`
- `setup-browser-cookies`
- `canary`
- `land-and-deploy`
- page-performance-oriented `benchmark`

## Phase 2: First CUDA Overlay

A separate `cuda-skills/` overlay was created at first. The idea was to keep upstream gstack untouched and add simulation-oriented skills beside it.

### First added materials

The following initial adaptation files were created:

- `CLAUDE.md`
- `CUDA_GSTACK_ADAPTATION.md`
- `docs/simulation-workflow.md`
- `docs/verification-matrix.md`
- `cuda-skills/cuda-dev/SKILL.md`
- `cuda-skills/cuda-investigate/SKILL.md`
- `cuda-skills/cuda-review/SKILL.md`
- `cuda-skills/cuda-benchmark/SKILL.md`
- `cuda-skills/cuda-verify/SKILL.md`
- `cuda-skills/cuda-release/SKILL.md`

### Purpose of those early CUDA skills

They encoded the simulation-specific development priorities:

1. mathematical correctness
2. memory safety and race freedom
3. numerical stability and convergence
4. reproducibility
5. performance
6. developer convenience

They also established the idea that compilation alone is not evidence, and that correctness claims should be backed by verification cases and, when relevant, benchmarks.

## Phase 3: Adapting Higher-Level Skills

The next step was to adapt high-level planning skills, not just implementation and review skills.

Two new CUDA-focused planning skills were introduced in the overlay phase:

- `cuda-office-hours`
- `cuda-plan-eng-review`

### Intent of `cuda-office-hours`

This was designed to reframe R&D and solver ideas into the narrowest high-value wedge before coding. Instead of product brainstorming, it focused on questions like:

- what exact solver limitation exists now
- what smallest change produces measurable value
- whether the gain is in accuracy, stability, robustness, runtime, or memory
- what benchmark or verification case can falsify the idea cheaply
- what larger roadmap the idea unlocks if it succeeds

### Intent of `cuda-plan-eng-review`

This was designed as an engineering review for simulation implementation plans, with focus on:

- governing equations and discretization consistency
- host/device data ownership
- kernel decomposition and race risks
- convergence and timestep limits
- verification strategy
- benchmark strategy
- backward compatibility and rollout risk

## Phase 4: Recognizing Overlay Limitations

After the first overlay version was created, an important structural issue was identified.

The original gstack skills are not just isolated markdown files. They also depend on:

- frontmatter structure
- common preamble conventions
- telemetry handling
- hooks
- generation from `.tmpl` templates
- documentation and indexing
- host-specific generated skill outputs

This meant the first `cuda-skills/` overlay was useful conceptually, but not fully equal to upstream gstack in terms of tooling integration.

## Phase 5: Upgrading CUDA Skills to gstack-Compatible Skill Format

The overlay skills were then promoted into gstack-style `SKILL.md` form.

### What was added to the CUDA skills

The upgraded CUDA skills were rewritten to include:

- YAML frontmatter
- `allowed-tools`
- gstack-style preamble patterns
- telemetry conventions
- completion status protocol
- freeze hook reuse for `cuda-investigate`

The following upgraded CUDA skills existed in this phase:

- `cuda-office-hours`
- `cuda-plan-eng-review`
- `cuda-dev`
- `cuda-investigate`
- `cuda-review`
- `cuda-benchmark`
- `cuda-verify`
- `cuda-release`

## Phase 6: Moving from Overlay to Upstream-Style Integration

After that, the repository moved from a sidecar overlay model to an upstream-style integrated model.

### New integrated skill directories inside `gstack/`

The CUDA skills were added directly into the vendored `gstack/` tree as first-class skill directories:

- `gstack/cuda-office-hours/`
- `gstack/cuda-plan-eng-review/`
- `gstack/cuda-dev/`
- `gstack/cuda-investigate/`
- `gstack/cuda-review/`
- `gstack/cuda-benchmark/`
- `gstack/cuda-verify/`
- `gstack/cuda-release/`

Each received both:

- `SKILL.md.tmpl`
- `SKILL.md`

### Additional documentation added during integration

- `gstack/CUDA_EXTENSION.md`
- CUDA extension sections appended to `gstack/README.md`
- CUDA extension section appended to `gstack/docs/skills.md`

### Root routing updates

The root gstack routing text in:

- `gstack/SKILL.md`
- `gstack/SKILL.md.tmpl`

was updated so that CUDA and numerical-simulation tasks suggest the new CUDA skills as first-class workflow options.

## Phase 7: Validation of the Integrated Skill System

The integrated CUDA skills were then validated using the gstack generation and skill checking pipeline.

### Prerequisites installed for validation

The environment did not initially have Bun available. Bun was installed locally by downloading the release zip and extracting it into `~/.bun/bin/bun`.

After that:

- gstack dependencies were installed with `bun install`
- `bun run gen:skill-docs` was executed
- `bun run gen:skill-docs --host codex` was executed
- `bun run skill:check` was executed

### Validation result

The validation passed.

Observed result:

- CUDA skill templates were accepted by the generator
- Claude-host generated skill files were fresh
- Codex-host generated skill files were fresh after regeneration
- `skill:check` finished successfully
- Codex skill inventory increased to include the new CUDA skills

Warnings about missing `$B` commands on some non-browser skills were not treated as failures, because they are normal for non-browser workflow skills.

## Phase 8: Removing the Old Overlay

Once upstream-style integration was working, the original `cuda-skills/` overlay was removed.

The repository then relied only on the integrated CUDA skills under `gstack/`.

The root `CLAUDE.md` was rewritten to reflect the new reality:

- CUDA skills are first-class and live inside the vendored `gstack/`
- root routing now points to the integrated CUDA skill set rather than a local overlay

## Phase 9: Publishing to GitHub

The repository was then prepared for publishing to GitHub.

### Remote used

The target GitHub repository was:

- `https://github.com/constlearner89/gstack-cuda.git`

### Initial git issues discovered and resolved

Several problems appeared during the first publication attempt:

1. the project root was not yet a git repository
2. `gstack/` still behaved like an embedded repository/gitlink initially
3. local git author identity was unset

### Fixes applied

- initialized the root repository with `git init -b main`
- added remote `origin`
- configured local git identity for the repo
- removed the nested `gstack/.git`
- replaced the accidental gitlink with vendored real files

### Publishing result

The repository was pushed successfully to GitHub.

A corrective follow-up push ensured that `gstack/` was committed as actual files rather than as a gitlink.

## Phase 10: Repository Cleanup and Presentation Polish

After the repository was online, the structure and presentation were refined.

### Cleanup work

The following were cleaned up:

- removed tracked `.agents` generated Codex skill outputs from `gstack/.agents/skills/`
- updated `gstack/.gitignore` to ignore `.agents/`
- removed local `gstack/node_modules`

### Added root landing README

A new root-level `README.md` was created so that the GitHub landing page clearly presents the repository as:

- `gstack-cuda`
- a CUDA/C++ numerical-simulation fork of gstack

### Rewrote vendored `gstack/README.md` header

The top of `gstack/README.md` was rewritten so that the repository identity is simulation-first rather than web-product-first.

This new header now explains:

- what the fork is
- what CUDA skills were added
- what simulation workloads it is intended for
- what original gstack methodology is preserved
- how the repository is laid out

### Updated quick-start section

The quick-start section in `gstack/README.md` was changed to prefer the CUDA workflow:

1. `/cuda-office-hours`
2. `/cuda-plan-eng-review`
3. `/cuda-review`
4. `/cuda-verify`
5. `/cuda-benchmark`

instead of the original web-oriented `office-hours -> review -> qa` flow.

## Final State

At the end of this work, the repository became a published GitHub fork with the following characteristics:

### Identity

- repository name: `gstack-cuda`
- purpose: CUDA/C++ numerical simulation workflows

### Core structure

- root-level project docs describe simulation adaptation
- vendored `gstack/` contains the upstream code plus integrated CUDA skill directories
- CUDA skills are first-class, generator-compatible, and documented

### CUDA skills integrated into gstack

- `/cuda-office-hours`
- `/cuda-plan-eng-review`
- `/cuda-dev`
- `/cuda-investigate`
- `/cuda-review`
- `/cuda-benchmark`
- `/cuda-verify`
- `/cuda-release`

### Validation status

- generation pipeline executed successfully
- skill health check passed
- both Claude and Codex generated skill outputs were validated during development

### GitHub state

The repository was pushed successfully to:

- `https://github.com/constlearner89/gstack-cuda.git`

## Important Design Principles Established During This Work

The following principles now define the fork:

- simulation work is the default, not web work
- correctness is more important than convenience
- compilation is never enough evidence
- numerical claims should be backed by deterministic verification and, where relevant, benchmarks
- solver planning and review should explicitly consider discretization, invariants, stability, race freedom, and representative workloads
- upstream compatibility matters, so CUDA skills were integrated using the same general skill layout and generator conventions as gstack
