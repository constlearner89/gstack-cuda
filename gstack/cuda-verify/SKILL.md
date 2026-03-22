---
name: cuda-verify
version: 1.0.0
description: |
  Verification workflow for numerical simulation repositories. Organizes
  evidence from algebra checks, small deterministic cases, regressions, and
  representative workloads. Use when asked to verify correctness.
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

## Verification Pyramid

1. algebra and utility tests
2. small deterministic physical cases
3. regression examples
4. larger representative workloads

## Evidence To Prefer

- manufactured solution checks
- conservation checks
- symmetry checks
- analytical or semi-analytical comparisons
- CPU/GPU agreement where applicable
- residual or convergence history

## Reject Weak Evidence

Do not treat these as sufficient on their own:
- code compiles
- visualization looks plausible
- one large run did not crash

## Telemetry (run last)

```bash
_TEL_END=$(date +%s)
_TEL_DUR=$(( _TEL_END - _TEL_START ))
~/.claude/skills/gstack/bin/gstack-telemetry-log \
  --skill "cuda-verify" --duration "$_TEL_DUR" --outcome "success" \
  --used-browse "false" --session-id "$_SESSION_ID" 2>/dev/null &
```
