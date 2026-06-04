---
name: prompt-intent
description: Write, revise, or review concise prompts and prompt-like instructions for coding agents. Use when drafting or evaluating system/developer prompts, skills, tool descriptions, command prompts, agent workflows, evaluation rubrics, or any text an agent will read to decide what to do, what context matters, which rules bind it, or how much freedom it has.
---

# Prompt Intent

## Overview

Use this skill to make prompts small enough to maintain and clear enough to execute. Treat skills, tool descriptions, commands, workflow specs, rubrics, and system or developer instructions as prompts when an agent will use them as context.

## Find The Boundary

Before writing or reviewing, identify the execution context:

- Which agent will read this prompt.
- Which prompt surfaces are already in context.
- Which tools, schemas, code, files, memories, or policies the agent can already see.
- Which facts come from the prompt writer's context but will be absent when the prompt runs.
- Whether the text should shape judgment, select tools, enforce a format, provide domain facts, or set a boundary.

Separate the writer's context from the executing agent's context. Do not assume a future agent can see the conversation that produced the prompt.

## Write By Intent

Draft in this order:

1. State the purpose and desired end state.
2. Add the minimum context needed to make good decisions.
3. Add constraints that genuinely bind the task.
4. Name the degrees of freedom the agent should keep.
5. Put deterministic checks in code, schemas, tests, permissions, or validators when possible.

Prefer intent over procedure when many good paths exist. Prefer procedure when the work is fragile, externally constrained, or easy to verify mechanically.

## Apply Min Specs

For every sentence or rule, ask:

- Would the agent likely fail without this?
- Does it hold across the intended scope?
- Is it already supplied by another prompt, tool description, schema, policy, or code path?
- Is it a real invariant, or only a useful heuristic?
- Could it live in a narrower prompt surface closer to where it matters?

Delete the sentence when it is not needed. Soften it when exceptions are plausible. Keep hard words such as `must`, `always`, `never`, and `only` for invariants, policies, or explicitly chosen scope limits.

## Assume A Smart Agent

Give the agent missing context, intent, constraints, examples, and validation targets. Avoid explaining obvious reasoning, repeating tool documentation, adding motivational filler, or spelling out generic competence.

Use examples only when they calibrate a non-obvious judgment, edge case, output shape, or tone. Prefer one realistic example over several toy examples.

## Review Prompts

When reviewing an existing prompt:

1. Inventory every prompt surface that may interact with it, including skills and tool descriptions.
2. Restate the intended behavior in one sentence.
3. Flag missing execution context, boundary confusion, over-broad hard rules, redundant instructions, stale assumptions, and instructions that belong in code or tools.
4. Mark each recommendation as `delete`, `soften`, `move`, `keep`, or `add`.
5. Provide a revised prompt when the requested outcome is clear.

Lead with the highest-risk findings. Keep style edits secondary unless wording changes behavior.

## Output Shape

For prompt drafting, return:

- `Intent`
- `Execution context`
- `Prompt draft`
- `Min Specs notes`

For prompt review, return:

- `Findings`
- `Recommended edits`
- `Revised prompt` when useful
