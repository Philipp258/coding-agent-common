---
name: cmux
description: Manage cmux workspaces, panes, surfaces, browser panels, task titles, and long-running visible processes. Use when running inside cmux or when a user asks to use cmux, manage app/test/log processes in cmux, open or inspect browser panels, organize workspace surfaces, recover cmux state, or keep development work visible outside the chat terminal.
---

# cmux

Use cmux as the visible workspace when it is available. Keep chat for agent interaction. Put app servers, test watchers, logs, and browser checks in named cmux surfaces.

## First Check

- If `cmux` is available, run `cmux identify --json` to learn the current workspace, window, pane, and surface.
- Set a short task title early. Prefer a project helper when one exists; otherwise use `cmux rename-workspace "short task"` or `cmux rename-tab "short task"`.
- Read repo instructions for cmux slots, ports, startup helpers, and browser conventions before starting services.
- If `cmux` is unavailable, say so and fall back to the normal local tools.

## Surfaces

- Reuse a named surface when it fits the task.
- Create separate surfaces for distinct jobs such as app server, tests, logs, browser, or scratch terminal.
- Prefer project helpers for startup; they know ports, env files, and surface names.
- If there is no helper, use cmux primitives:

```bash
cmux new-surface --type terminal --workspace <workspace>
cmux rename-tab --surface <surface> "dev log"
cmux send --surface <surface> "<command>"
cmux send-key --surface <surface> Enter
```

- Check existing ports or health URLs before starting another server.

## Browser

- Open or reuse a browser surface with `cmux browser open <url>` or `cmux browser goto <url>`.
- Keep browser state in the same workspace as the process it is testing.
- Verify frontend changes with focused browser actions such as `snapshot`, `screenshot`, `wait`, `click`, `fill`, `press`, `console list`, and `errors list`.
- Use the Browser plugin when it is available and better suited to the inspection.

## Process Hygiene

- Avoid long-lived processes in the chat terminal.
- Name surfaces by task or function.
- Tell the user which useful surfaces, URLs, or processes remain running.
- Reuse or stop conflicting processes before starting duplicates.

## Recovery

If cmux commands fail because the socket or app is unavailable, avoid repeated retries. Check availability, use the project helper's recovery command when present, or ask the user to reopen cmux.
