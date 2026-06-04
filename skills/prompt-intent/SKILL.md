---
name: prompt-intent
description: Use this whenever you work with instructions that an agent might follow in any way. E.g. when drafting or evaluating system/developer prompts, skills, tool descriptions, command prompts, agent workflows or evaluation rubrics
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

Unless surely you know the agent following the prompt is not intelligent, assume it it.
Give the agent missing context and intent and only the minimum info necessary to achieve the goal.
Assume it is capable and smart.

