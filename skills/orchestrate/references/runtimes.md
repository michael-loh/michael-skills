# Runtime adapters

Read the section for the current host. Live tool schemas and higher-priority instructions take precedence over these examples. Model names are preferences to resolve against available controls, not guaranteed access. Do not launch separate paid API sessions or install tooling just to obtain a preferred model without authorization.

## Codex

Use the host's native subagent tools when exposed. Some hosts support per-spawn `model` and `reasoning_effort`; others use configured agent roles or inherit the parent's settings. Inspect the actual interface rather than assuming a tool name or argument. Prefer the available Sol variant for standard work, Luna for economy work, and Astra for premium plan review. In a host exposing `gpt-6.1-sol`, `gpt-6-luna`, and `gpt-6-astra`, those satisfy the requested routing preferences.

When per-spawn overrides require a fresh context, use that mode (for example `fork_turns: "none"`) and supply a self-contained brief. Some Codex configurations recommend high effort for Luna and low for Astra; choose supported settings based on task and host guidance rather than treating effort names as comparable token budgets across models.

If only inherited-model workers are supported, continue using those workers and disclose the routing limitation once. Do not claim heterogeneous routing occurred. Do not modify global configuration or create custom agent definitions merely to enforce preferences unless that setup is requested.

Installation: copy this whole `orchestrate` folder into a skill location supported by the client, such as the user's `~/.codex/skills/` or a repository's `.agents/skills/`. Invoke as `$orchestrate <normal prompt>` or select it in the client's skill picker. Slash-command UI support varies by client. Read the client's current documentation if discovery fails.

## Claude Code

Use the available native subagent interface. Prefer Haiku for economy work, Sonnet for implementation and detailed review, and Opus for bounded high-level plan review. Resolve aliases and per-invocation effort against the current tool schema; older clients may require configured agent definitions or may not support effort overrides. Session policies and environment settings can force a model or effort.

Do not set `context: fork` on this skill: it should direct the human-facing main agent. Spawn workers from that main agent. Use an execution-capable worker for implementation; a read-only Explore agent cannot make changes. Do not assume workers receive the skill or full parent conversation; pass their assignment, constraints, and instruction locations explicitly.

Installation: copy this whole `orchestrate` folder to `~/.claude/skills/orchestrate/` for personal use or `.claude/skills/orchestrate/` in a project. Invoke `/orchestrate <normal prompt>`. Claude appends invocation arguments even without a placeholder in the skill body.

## Sources

Runtime guidance verified November 5, 2026. Recheck when the host interface changes.

- [Codex subagents](https://learn.chatgpt.com/docs/agent-configuration/subagents)
- [Claude Code subagents](https://code.claude.com/docs/en/sub-agents)
- [Claude Code skills](https://code.claude.com/docs/en/skills)
