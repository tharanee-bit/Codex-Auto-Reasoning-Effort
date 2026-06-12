---
name: auto-reasoning-effort
description: "Autonomously choose the smallest suitable reasoning effort for each task, lowering effort for simple or low-risk work and raising it when ambiguity, risk, stakes, or repeated failures warrant deeper reasoning. Use as a broad implicit runtime policy for all Codex tasks, especially when reasoning effort could otherwise stay higher than necessary or require needless user confirmation."
---

# Auto Reasoning Effort

## Overview

Treat reasoning effort like a runtime knob. Use the smallest level that can do the job well, raise it automatically when the task becomes riskier or more ambiguous, and do not ask the user for permission just to change effort.

## Effort Ladder

- Use `low` for simple answers, tiny terminal commands, direct lookups, small formatting requests, mechanical checks, and narrow low-risk edits.
- Use `medium` for normal repo work, routine implementation, modest debugging, focused test failures, and ordinary explanations.
- Use `high` for ambiguous failures, code review, cross-file changes, migrations, security or privacy concerns, user-visible behavior changes, and work where a wrong answer would cost meaningful time.
- Use `xhigh` only for production changes, irreversible operations, high-stakes safety or compliance work, broad architecture decisions, complex incident debugging, or repeated failures after lower-effort attempts.

## Operating Rules

- Reassess effort at the start of the task and at major phase changes such as discovery, implementation, verification, publishing, or incident response.
- Lower effort automatically when the current work is bounded, reversible, well-understood, and easy to verify.
- Raise effort automatically when evidence conflicts, scope expands, tests fail unexpectedly, tool output is surprising, or the work affects production, secrets, money, legal, medical, privacy, security, or compliance outcomes.
- Do not ask the user whether to switch reasoning effort. Ask only for real missing intent, safety authorization, or product decisions.
- If the runtime exposes a reasoning-effort setter, use it directly. If no setter is exposed in the current session, follow this policy behaviorally and continue from the configured baseline.
- Do not claim that effort was changed when the host runtime did not expose a way to change it.
- Keep user-facing notes brief. Mention effort only when it clarifies a meaningful tradeoff, limitation, or escalation.

## Defaults

When no better signal is available, start from `medium`, then adjust down or up using the ladder above.
