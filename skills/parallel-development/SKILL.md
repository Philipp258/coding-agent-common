---
name: parallel-development
description: Use when setting up, documenting, or working in a parallel local app-development workflow with fixed worktree slots, isolated app instances, cmux workspaces, per-slot ports/env/state, stable IDE indexes, and coding-agent sessions.
---

# Parallel Development

Use this pattern for local app work where multiple tasks should progress in
parallel without constantly recreating environments.

## Principle

Prefer a fixed set of long-lived development slots over disposable worktrees.
Each slot should have a stable worktree, branch, env file, ports, runtime state,
IDE index, and cmux workspace. Reuse slots for routine local work; create or
delete worktrees only when explicitly requested.

The app should be able to run multiple isolated copies. Containerization is one
way to achieve that, but the real requirement is isolation: separate ports,
state, data stores, service names, cache dirs, secrets, and URLs per slot.

Keep the default state lightweight. A slot should be ready for work, but the app
does not need to be running until a task needs live behavior.

## Slot Contract

For each project, define the slot contract in the repo instructions:

- slot count and slot naming
- path and branch pattern
- env file location and setup command
- app start command
- health URL and primary frontend URL
- per-slot port, database, data, and cache formulas
- any IDE/open command
- any helper commands for `list`, `up`, `dev`, `title`, or `doctor`

Prefer deterministic formulas over per-slot prose when possible. Example:
backend port `BASE_BACKEND_PORT + slot - 1`.

## cmux Contract

Use one cmux workspace or vertical tab per slot. The first surface should be the
coding agent, already placed in that slot worktree.

When live app behavior is needed, create or reuse named surfaces in the same
workspace:

- `dev log` for the long-running app process
- `browser` for the primary frontend URL
- optional short-lived shell surfaces for manual inspection

Keep logs, browser state, and agent context in the slot workspace they belong to.
Do not run long-lived app processes in the coding-agent chat surface.

## Agent Workflow

At the start of a task:

1. Identify the current project, slot, and cmux context.
2. Set a short cmux workspace or vertical-tab title for the task.
3. Check whether the app is already running before starting another copy.

During the task:

- Assume work is happening inside a fixed slot unless the environment clearly
  says otherwise.
- Use project helpers before generic cmux commands; helpers know the slot ports,
  env files, and surface names.
- Start the app on demand only when live backend/frontend behavior is useful.
- If the slot is partially running, investigate before forcing another start.
- Use the browser surface or Browser plugin for frontend verification.
- Leave the slot in a resumable state: title meaningful, logs visible, browser in
  the same workspace, and no unnecessary duplicate processes.

## Project Helper Shape

A good project helper usually supports:

- `up [slot|all]`: create or reuse lightweight slot workspaces
- `list`: show slot paths, ports, app status, and workspace ids
- `dev <slot>`: create/reuse log and browser surfaces, then start the app
- `title <slot> <title>`: set the cmux workspace title
- `doctor [slot|all]`: check slot prerequisites

Names can vary, but the behavior should be discoverable from `AGENTS.md`.
