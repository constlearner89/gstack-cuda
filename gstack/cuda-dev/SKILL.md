---
name: cuda-dev
version: 1.0.0
description: |
  Default implementation workflow for CUDA/C++ numerical simulation projects.
  Emphasizes mathematical correctness, memory safety, numerical stability,
  targeted verification, and explicit benchmark evidence. Use when asked to
  implement or modify CUDA/C++ numerical code.
allowed-tools:
  - Bash
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - AskUserQuestion
  - WebSearch
---
<!-- AUTO-GENERATED from SKILL.md.tmpl — do not edit directly -->
<!-- Regenerate: bun run gen:skill-docs -->

## Preamble (run first)

```bash
mkdir -p ~/.gstack/sessions
touch ~/.gstack/sessions/"$PPID"
_BRANCH=$(git branch --show-current 2>/dev/null || echo "unknown")
_TEL_START=$(date +%s)
_SESSION_ID="$$-$(date +%s)"
echo "BRANCH: $_BRANCH"
```

## Operating Rules

1. Identify governing equation or algorithmic goal.
2. Identify affected state variables, units, invariants, and stability limits.
3. Prefer local reasoning before broad refactors.
4. Never treat compilation alone as success.
5. Validate correctness before tuning performance.
6. Record exact build and verification commands.

For GPU changes, always consider:
- grid and block indexing
- boundary and halo handling
- shared and global memory lifetime
- race conditions and atomics
- occupancy and memory traffic

## Expected Deliverables

- code change
- verification note
- risk note if numerical behavior or tolerances changed

## Telemetry (run last)

```bash
_TEL_END=$(date +%s)
_TEL_DUR=$(( _TEL_END - _TEL_START ))
~/.claude/skills/gstack/bin/gstack-telemetry-log \
  --skill "cuda-dev" --duration "$_TEL_DUR" --outcome "success" \
  --used-browse "false" --session-id "$_SESSION_ID" 2>/dev/null &
```
