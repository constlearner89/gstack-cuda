---
name: cuda-investigate
version: 1.0.0
description: |
  Root-cause investigation for CUDA/C++ simulation failures such as crashes,
  NaNs, divergence, conservation loss, CPU/GPU mismatch, and unexpected
  performance regressions. Use when asked to debug or investigate solver bugs.
allowed-tools:
  - Bash
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - AskUserQuestion
  - WebSearch
hooks:
  PreToolUse:
    - matcher: "Edit"
      hooks:
        - type: command
          command: "bash ${CLAUDE_SKILL_DIR}/../../gstack/freeze/bin/check-freeze.sh"
          statusMessage: "Checking debug scope boundary..."
    - matcher: "Write"
      hooks:
        - type: command
          command: "bash ${CLAUDE_SKILL_DIR}/../../gstack/freeze/bin/check-freeze.sh"
          statusMessage: "Checking debug scope boundary..."
---
<!-- AUTO-GENERATED from SKILL.md.tmpl — do not edit directly -->
<!-- Regenerate: bun run gen:skill-docs -->

## Preamble (run first)

```bash
_UPD=$(~/.claude/skills/gstack/bin/gstack-update-check 2>/dev/null || .claude/skills/gstack/bin/gstack-update-check 2>/dev/null || true)
[ -n "$_UPD" ] && echo "$_UPD" || true
mkdir -p ~/.gstack/sessions
touch ~/.gstack/sessions/"$PPID"
_BRANCH=$(git branch --show-current 2>/dev/null || echo "unknown")
_TEL_START=$(date +%s)
_SESSION_ID="$$-$(date +%s)"
echo "BRANCH: $_BRANCH"
mkdir -p ~/.gstack/analytics
echo '{"skill":"cuda-investigate","ts":"'$(date -u +%Y-%m-%dT%H:%M:%SZ)'","repo":"'$(basename "$(git rev-parse --show-toplevel 2>/dev/null)" 2>/dev/null || echo "unknown")'"}' >> ~/.gstack/analytics/skill-usage.jsonl 2>/dev/null || true
```

## Iron Law

No fix without a root-cause hypothesis.

## Phases

1. Investigate
   - exact input case
   - exact build flags
   - GPU and driver assumptions
   - first bad timestep, iteration, particle, or cell if known
2. Analyze
   - indexing or bounds error
   - lifetime or ownership bug
   - race condition
   - bad initialization
   - unstable timestep or solver setting
   - constitutive or flux bug
   - precision loss or cancellation
   - invalid boundary condition
3. Hypothesize
   - write the smallest falsifiable explanation
4. Implement
   - apply the smallest change that proves or disproves the hypothesis

## Required Evidence

Before closing the bug, show at least one of:
- crash removed and target case passes
- NaN source identified and eliminated
- invariant restored within tolerance
- performance regression explained and recovered

## Completion Status Protocol

Use one of:
- DONE
- DONE_WITH_CONCERNS
- BLOCKED
- NEEDS_CONTEXT

## Telemetry (run last)

```bash
_TEL_END=$(date +%s)
_TEL_DUR=$(( _TEL_END - _TEL_START ))
~/.claude/skills/gstack/bin/gstack-telemetry-log \
  --skill "cuda-investigate" --duration "$_TEL_DUR" --outcome "success" \
  --used-browse "false" --session-id "$_SESSION_ID" 2>/dev/null &
```
