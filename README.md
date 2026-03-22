# gstack-cuda

A CUDA/C++ numerical-simulation fork of `gstack`.

This repository vendors `gstack` and extends it with first-class skills for simulation engineering:

- CUDA kernel development
- DEM, SPH, FVM, FEM, CFD, and multiphysics solver work
- numerical debugging and verification
- benchmarking and release discipline for solver code

## Start Here

- Fork overview: [`gstack/README.md`](gstack/README.md)
- Simulation extension summary: [`gstack/CUDA_EXTENSION.md`](gstack/CUDA_EXTENSION.md)
- Project routing instructions: [`CLAUDE.md`](CLAUDE.md)
- Adaptation notes: [`CUDA_GSTACK_ADAPTATION.md`](CUDA_GSTACK_ADAPTATION.md)
- Local workflow docs: [`docs/simulation-workflow.md`](docs/simulation-workflow.md)

## Integrated CUDA Skills

- `/cuda-office-hours`
- `/cuda-plan-eng-review`
- `/cuda-dev`
- `/cuda-investigate`
- `/cuda-review`
- `/cuda-benchmark`
- `/cuda-verify`
- `/cuda-release`

## Notes

The vendored upstream code lives in `gstack/`. The CUDA extension is integrated into that tree in upstream-style skill directories rather than maintained as a separate overlay.
