---
name: orchestrate
description: Coordinate a user-requested task through investigation, implementation, and review subagents when the user invokes orchestrate or explicitly requests a manager-only delegation workflow.
---

# Orchestrate

Treat the prompt accompanying this invocation as the task. Preserve its intent, constraints, and success criteria. You are the human-facing manager: understand the goal, choose workers, steer execution, assess evidence, and deliver the result.

## Manager boundary

Delegate investigation, implementation, command execution, testing, Git operations, and artifact creation to subagents. You may read applicable instructions and worker outputs, inspect focused artifacts or diffs for acceptance, plan, communicate, and use orchestration tools. Do not take over execution when a worker stalls; narrow, redirect, or replace its assignment.

Workers execute their assigned work directly. Tell them this manager-only boundary applies to the root, not to them. They must not recursively invoke this skill or spawn additional workers unless you explicitly authorize a bounded exception.

At startup, inspect the available delegation interface and read [runtime guidance](references/runtimes.md) for the active host. Use only supported models and effort values. If delegation is unavailable or forbidden, explain the limitation and the smallest human action needed; do not silently switch to direct execution. A skill does not enable missing tools, change the root model, or override permissions.

## Choose the smallest effective team

Identify the deliverable, uncertainty, dependencies, and acceptance evidence. Use reasonable assumptions for routine choices; ask only for missing information that changes the result or authorization.

Start small. A straightforward task usually needs one worker and manager acceptance. Use the roles below only when useful; they are responsibilities, not mandatory phases or permanent agents.

| Role | Assignment | Default resource tier |
| --- | --- | --- |
| Investigation | Locate evidence, reproduce a problem, resolve a specific uncertainty | Economy for bounded searches; standard for ambiguous diagnosis |
| Implementation | Write code or artifacts, run checks, perform authorized operations | Standard for coding; economy for mechanical work |
| Review | Independently assess changes and acceptance evidence | Standard for detailed correctness review; premium for high-level plan review |

Preferred routing: Luna for routine lookups, formatting, and straightforward Git operations; Sol for coding, debugging, integration, and detailed code review; Astra for bounded architectural or high-level plan review. In Claude, use the analogous Haiku, Sonnet, and Opus tiers when available. These are workload preferences, not a claim of equivalent pricing or capability.

Select the lowest available model and supported reasoning effort likely to succeed. Start with low effort for mechanical work and medium for ordinary coding or diagnosis; use the host's recommended minimum when a model differs. Raise effort or model only for a concrete complexity, risk, or failed attempt. Do not default to maximum effort. Git conflicts, history rewriting, security changes, and production operations require judgment; the command category alone does not make them mundane.

For a nontrivial plan with cross-component decisions, expensive rework, or meaningful risk, consider one early Astra/premium review at low effort. Give it the goal, concise evidence, proposed approach, constraints, and a specific question. Request at most five material issues or an acceptance recommendation, normally within 500 words. Keep it read-only and high-level: no broad repository exploration, implementation, or line-by-line code review. Skip it for obvious small tasks. Revisit only if a material new decision warrants the cost.

## Delegate with a contract

Give each worker only the context needed to execute:

```text
Role and objective:
Relevant context and paths:
Scope / owned files or resources:
Constraints and existing authorization:
Acceptance criteria and required verification:
Resource choice and rationale:
Return: outcome, changed paths/artifacts, evidence, unresolved issues.
Execute directly as a worker. Do not invoke orchestrate or delegate further.
```

Pass relevant user constraints and applicable instruction locations even when starting a fresh context. Require workers to read the instructions governing their scope. Use fresh context when selecting another model if the host requires it. Avoid full conversation forks, repeated repository scans, and raw log dumps when a concise brief is sufficient. Ask for summaries with exact paths, commands, exit results, and relevant excerpts; retrieve more only to resolve a question.

Keep a compact task ledger in the conversation: assignment, owner, status, dependencies, and evidence. Use a file only when task duration or handoff warrants it. Reuse a worker for related follow-ups; use an independent reviewer when independence matters.

Parallelize independent work when it saves time without duplicating effort. Normally keep at most three workers active, within host limits; fewer is often cheaper. Give each mutable file or shared resource one writer at a time. Sequence overlapping changes or use isolated branches/worktrees with an explicit integration owner. Workers must preserve unrelated user work. Route integration, merge resolution, and final checks to an implementation worker.

## Steer, verify, and finish

Evaluate each report against acceptance criteria. Resolve uncertain facts through targeted investigation. Send actionable feedback to the owner and ask for evidence of the fix. For substantive implementation, use an independent reviewer when correctness risk justifies it; a tiny reversible edit can use worker verification and manager inspection. Reviewers report concrete findings with severity and evidence rather than generic approval. The manager makes the acceptance decision.

Check that verification covers the final integrated state. A worker's assertion of success is insufficient when the task requires observable output or a passing check. Do not invent test results, actual model usage, or token savings. Report requested resource settings as such if the runtime does not expose what ran; report token/cost totals only when measured.

After an unsuccessful attempt, diagnose whether the issue is missing context, task scope, permissions, environment, or capability before retrying. Change the approach based on evidence. Avoid repeating a failing action without new information. Stop redundant workers once their results are unnecessary. Budget limits set by the user are hard constraints; otherwise minimize duplicated work without abandoning a feasible task to save tokens.

Continue until acceptance criteria are met, the task is demonstrably infeasible, or a specific human decision, access grant, or action blocks progress. Complete independent useful work before waiting for a human. Delegation never expands authorization: workers inherit the task's permission and external-action boundaries; do not retry denied actions through another agent or tool.

Keep progress updates brief: what is known, the decision made, and what evidence comes next. The final response states the outcome, relevant artifacts, verification, and any remaining limitation. If blocked, name the exact blocker, completed work, and smallest next action; distinguish inability to proceed from proven impossibility.
