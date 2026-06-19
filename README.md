# Auto Reasoning Effort (Codex skill)

A [Codex](https://github.com/openai/codex) skill that treats reasoning effort like a runtime knob:
use the smallest level that does the job well, raise it automatically when the task gets riskier or
more ambiguous, and never stop to ask the user for permission just to change effort.

It is the Codex-native counterpart of the Claude Code `auto-reasoning-effort` skill.

## Why

Leaving reasoning effort pinned high wastes time and tokens on trivial work; pinning it low produces
shallow answers on hard work. This skill makes the level track the task instead, so simple edits stay
fast and ambiguous, high-stakes, or repeatedly-failing work gets deeper reasoning.

## The effort ladder

- **`low`** - simple answers, tiny terminal commands, direct lookups, mechanical checks, narrow low-risk edits.
- **`medium`** - normal repo work, routine implementation, modest debugging, focused test failures, ordinary explanations. *(default when no better signal exists)*
- **`high`** - ambiguous failures, code review, cross-file changes, migrations, security/privacy concerns, user-visible behavior changes.
- **`xhigh`** - production changes, irreversible operations, high-stakes safety/compliance work, broad architecture decisions, repeated failures after lower-effort attempts.

Effort is reassessed at the start of a task and at major phase changes (discovery, implementation,
verification, publishing, incident response). See [`SKILL.md`](SKILL.md) for the full operating rules.

## Install

Place this directory where your Codex install discovers skills (the skill is identified by
[`SKILL.md`](SKILL.md); [`agents/openai.yaml`](agents/openai.yaml) supplies the display name and allows
implicit invocation). Then invoke it explicitly with `$auto-reasoning-effort`, or let it load
implicitly as a broad runtime policy.

## License

[MIT](LICENSE)
