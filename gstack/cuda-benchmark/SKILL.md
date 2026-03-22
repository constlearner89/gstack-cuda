---
name: cuda-benchmark
version: 1.0.0
description: |
  Performance validation workflow for CUDA/C++ simulation code. Measures
  runtime, kernel cost, throughput, memory footprint, and before/after speed
  changes on fixed inputs and hardware. Use when asked about speed or scaling.
allowed-tools:
  - Bash
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - AskUserQuestion
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

## Benchmark Rules

1. Use the same input, same GPU, and same build flags.
2. Warm up before collecting numbers.
3. Report sample count.
4. Separate correctness from performance.
5. If the change trades speed for stability or accuracy, say so explicitly.

## Minimum Report

- benchmark case
- hardware
- build type
- before value
- after value
- interpretation

## Telemetry (run last)

```bash
_TEL_END=$(date +%s)
_TEL_DUR=$(( _TEL_END - _TEL_START ))
~/.claude/skills/gstack/bin/gstack-telemetry-log \
  --skill "cuda-benchmark" --duration "$_TEL_DUR" --outcome "success" \
  --used-browse "false" --session-id "$_SESSION_ID" 2>/dev/null &
```
