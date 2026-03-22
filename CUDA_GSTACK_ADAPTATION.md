# CUDA/C++ Gstack Adaptation

This repository was originally designed around web-product workflows. This adaptation keeps the useful parts of gstack's methodology and rewrites them for CUDA/C++ numerical simulation work.

## Goal

Use the repository as an operating system for:

- CUDA/C++ solver development
- DEM, SPH, FVM, FEM implementations
- numerical debugging and regression control
- performance-focused review and release discipline

## What To Keep From gstack

These parts transfer well with little change:

- `investigate`: root-cause-first debugging
- `review`: structured pre-landing review
- `ship`: explicit pre-merge validation
- `careful` and `freeze`: safety around edits
- `plan-eng-review`: architecture and execution review

These parts are web-specific and should become optional rather than default:

- `browse`
- `qa` for browser flows
- `benchmark` for page performance
- `setup-browser-cookies`
- `design-review`
- `design-consultation`
- `land-and-deploy` when there is no web deployment target

## Replacement Mental Model

Replace "browser + UX + deploy" with:

- build matrix
- solver correctness
- numerical stability
- conservation/invariants
- GPU memory correctness
- kernel performance
- reproducible experiments

## Recommended New Skill Set

Add domain-specific skills under `cuda-skills/`:

- `cuda-dev`: default development policy for CUDA/C++
- `cuda-investigate`: debug crashes, NaNs, divergence, unstable time stepping
- `cuda-review`: review for race conditions, indexing bugs, numerical mistakes, API misuse
- `cuda-benchmark`: profile kernels and compare before/after runtime
- `cuda-verify`: run physics and regression checks
- `cuda-release`: document solver, case, mesh, parameter, and benchmark changes

## Standard Workflow

1. Define the physics and acceptance criteria before editing.
2. Identify governing equations, discretization, state variables, units, and invariants.
3. Modify code in the smallest solver-local scope possible.
4. Build the exact target configuration.
5. Run correctness checks first.
6. Run performance checks second.
7. Record inputs, hardware assumptions, and numerical tolerances.
8. Only then prepare the final diff or release.

## Required Review Questions

Every meaningful change should answer:

- Is the discretization change mathematically consistent?
- Are boundary conditions still correct?
- Are indexing and ghost/halo accesses valid?
- Are units and normalization consistent?
- Can this introduce NaNs, negative density, negative volume, or energy blow-up?
- Did the CFL or iteration convergence condition change?
- Does the kernel have races, atomics contention, or undefined memory access?
- Is the result reproducible across seeds, block sizes, and GPU architectures?
- Did runtime improve, regress, or stay neutral?

## Verification Ladder

Use this order:

1. Compile-time checks: warnings, templates, flags, sanitizer-compatible host code.
2. Unit checks: geometry, constitutive relations, fluxes, kernels, neighbor search.
3. Small deterministic cases: one-particle, one-cell, patch, manufactured solution, cavity, beam, etc.
4. Regression cases: previously validated examples.
5. Performance cases: representative production-scale scenes.

## Minimal Directory Layout

You can layer this on top of any CUDA solver repo:

```text
cuda-skills/
  cuda-dev/
    SKILL.md
  cuda-investigate/
    SKILL.md
  cuda-review/
    SKILL.md
  cuda-benchmark/
    SKILL.md
  cuda-verify/
    SKILL.md
  cuda-release/
    SKILL.md
docs/
  simulation-workflow.md
  verification-matrix.md
  benchmark-log.md
```

## Environment Expectations

The adapted workflow assumes projects usually have some subset of:

- `CMakeLists.txt`
- `Makefile`
- `compile_commands.json`
- `tests/`
- `examples/`
- `benchmarks/`
- `docs/`

## Practical Rule

For CUDA/C++ code, "looks right" is not evidence.

Evidence means:

- it compiles
- it passes a targeted case
- it preserves expected invariants within tolerance
- it does not materially regress performance unless the tradeoff is explicit
