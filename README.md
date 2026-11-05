# Agent Skills

Personal skills for Codex and Claude Code. Each skill lives under `skills/<name>/` and includes a portable `SKILL.md` entrypoint.

## Orchestrate

Use any normal prompt with a manager-only agent that delegates execution, reviews evidence, and follows the work through completion or a concrete blocker.

```text
Codex:       $orchestrate Fix the upload retry bug and verify the behavior.
Claude Code: /orchestrate Fix the upload retry bug and verify the behavior.
```

The default resource policy is Luna / Sol / Astra in Codex and Haiku / Sonnet / Opus in Claude: economy for mechanical work, standard for coding and detailed review, premium for bounded high-level plan review. Small tasks use one worker. Available models and effort controls depend on the host; the skill cannot add missing capabilities or guarantee lower total cost.

## Install

Copy the complete `skills/orchestrate` directory into one of these locations:

| Client | Personal installation | Project installation |
| --- | --- | --- |
| Codex | `~/.codex/skills/orchestrate/` | `.agents/skills/orchestrate/` |
| Claude Code | `~/.claude/skills/orchestrate/` | `.claude/skills/orchestrate/` |

Use the path supported by your client and reload skill discovery or start a new session if needed. No API keys or global configuration changes are included. Invocation is intended to be explicit; the description targets an explicit orchestration request. Codex UI metadata is in `agents/openai.yaml`; the shared frontmatter uses standard skill fields.

See [the skill](skills/orchestrate/SKILL.md) and [runtime guidance](skills/orchestrate/references/runtimes.md) for behavior and host limitations.

## Maintenance

Keep the shared workflow in `SKILL.md` and host-specific details in references. Validate behavior with realistic prompts after changing routing or delegation rules. Model choice is a preference evaluated against the live host, not a pinned universal catalog.
