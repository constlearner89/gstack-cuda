# Simulation Workflow

This project uses gstack-style discipline adapted for CUDA/C++ simulation code.

## Default Task Flow

1. Clarify the physics and numerical target.
2. Inspect the local solver area before editing.
3. Make the smallest code change that can satisfy the target.
4. Build the exact affected target.
5. Run a small verification case.
6. Run a benchmark if a hot path changed.
7. Summarize outcome, evidence, and remaining risk.

## Example Acceptance Criteria

- DEM: contact force law stays stable and momentum drift is bounded
- SPH: density stays positive and pressure noise does not worsen materially
- FVM: residual converges and flux balance stays within tolerance
- FEM: displacement/stress field matches reference within tolerance
