# Project Instructions

This repository uses gstack-style operating discipline adapted for CUDA/C++ numerical software.

## Default Mode

Assume the primary work is one of:

- CUDA kernel development
- C++ solver implementation
- DEM, SPH, FVM, FEM, CFD, multiphysics, or linear solver work
- debugging crashes, NaNs, instability, or performance regressions

Do not assume this is a web project unless the user explicitly says so.

## Skill Routing

Prefer these gstack-integrated CUDA skills and workflows:

- `cuda-office-hours` for idea framing, narrowing scope, and R&D prioritization
- `cuda-plan-eng-review` for implementation planning and architecture review
- `cuda-dev` for normal implementation work
- `cuda-investigate` for bug investigation and root-cause analysis
- `cuda-review` for code review
- `cuda-benchmark` for performance work
- `cuda-verify` for correctness and regression evidence
- `cuda-release` before shipping solver changes

Use original gstack skills selectively:

- keep `investigate`, `review`, `ship`, `careful`, `freeze`, `guard`, and `plan-eng-review` as fallback tools
- treat browser, design, and web QA skills as optional and non-default
- when the user asks for `office-hours`, `plan-eng-review`, `review`, or release help, prefer the CUDA variants unless the task is clearly product or web oriented

## Compatibility Notes

The CUDA skills now live inside the vendored `gstack/` tree as first-class skills:

- `gstack/cuda-office-hours/SKILL.md`
- `gstack/cuda-plan-eng-review/SKILL.md`
- `gstack/cuda-dev/SKILL.md`
- `gstack/cuda-investigate/SKILL.md`
- `gstack/cuda-review/SKILL.md`
- `gstack/cuda-benchmark/SKILL.md`
- `gstack/cuda-verify/SKILL.md`
- `gstack/cuda-release/SKILL.md`

They are managed in the same upstream-style layout as other gstack skills, including:

- YAML frontmatter
- `allowed-tools` declarations
- gstack-compatible preamble and telemetry pattern
- completion status protocol
- freeze hook reuse for `cuda-investigate`

## Engineering Priorities

Order priorities like this:

1. mathematical correctness
2. memory safety and race freedom
3. numerical stability and convergence
4. reproducibility
5. performance
6. developer convenience

## Required Development Behavior

Before editing, identify:

- governing equations or algorithmic goal
- affected state variables and units
- likely invariants or conservation properties
- target build, test, or benchmark command

After editing, provide evidence from the strongest feasible level:

- compilation
- small deterministic verification case
- regression case
- benchmark if hot paths changed

Do not present compilation alone as proof of correctness.

## CUDA Review Heuristics

Always check for:

- thread and block indexing correctness
- out-of-bounds accesses
- race conditions and atomics misuse
- stale halo or ghost data
- wrong sign conventions in fluxes, gradients, or forces
- unit inconsistencies
- precision loss or unstable timestep selection
- unnecessary host-device transfers

## Communication

When reviewing or summarizing work, emphasize:

- what physical or numerical behavior changed
- how it was verified
- what remains risky or unverified
