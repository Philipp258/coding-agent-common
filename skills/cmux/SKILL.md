---
name: cmux
description: Use cmux's CLI to inspect and control windows, workspaces, panes, terminal surfaces, browser surfaces, focus, layout, settings, and browser automation. Use when a task mentions cmux, cmux browser panels, cmux workspaces, panes, surfaces, routing commands through cmux, reading or sending terminal input, opening URLs or files in cmux, or changing cmux-owned settings.
---

# cmux

cmux is controlled through the `cmux` CLI.

## Docs

Use cmux's own docs when command details matter:

```bash
cmux --help
cmux docs api
cmux docs browser
cmux docs settings
```

## Model

- Window: top-level macOS cmux window.
- Workspace: sidebar/tab-like group inside a window.
- Pane: split region inside a workspace.
- Surface: terminal or browser tab inside a pane.
- Handle: `window:N`, `workspace:N`, `pane:N`, or `surface:N`. UUIDs also work; request UUID output only when needed.

## Identify

Prefer caller context over visual focus:

```bash
cmux identify --json
cmux tree --all
cmux list-windows
cmux list-workspaces
cmux list-panes --workspace workspace:2
cmux list-pane-surfaces --workspace workspace:2 --pane pane:1
```

cmux terminals set `CMUX_WORKSPACE_ID`, `CMUX_SURFACE_ID`, and `CMUX_SOCKET_PATH`. Use those or refs from `identify`/`tree` as explicit `--workspace`, `--surface`, and `--window` targets for mutating commands.

## Layout

```bash
cmux new-workspace --name "name" --cwd "$PWD"
cmux new-pane --workspace workspace:2 --type terminal --direction right --focus false
cmux new-pane --workspace workspace:2 --type browser --direction right --url "https://example.com" --focus false
cmux new-surface --workspace workspace:2 --pane pane:1 --type terminal --focus false
cmux new-surface --workspace workspace:2 --pane pane:1 --type browser --url "https://example.com" --focus false
cmux move-surface --surface surface:7 --pane pane:2 --focus false
cmux reorder-surface --surface surface:7 --before surface:3
cmux close-surface --surface surface:7
```

`rename-workspace` names a workspace. `rename-tab` names a surface tab inside a pane.

## Terminal Surfaces

```bash
cmux read-screen --workspace workspace:2 --surface surface:7 --scrollback --lines 100
cmux send --workspace workspace:2 --surface surface:7 "npm test"
cmux send-key --workspace workspace:2 --surface surface:7 Enter
cmux surface-health --workspace workspace:2
cmux top --workspace workspace:2 --processes
```

## Browser Surfaces

Open or target one browser surface, verify navigation, snapshot, act, wait, then snapshot again.

```bash
cmux --json browser open "https://example.com"
cmux browser surface:7 get url
cmux browser surface:7 wait --load-state complete --timeout-ms 15000
cmux browser surface:7 snapshot --interactive
cmux browser surface:7 fill e1 "hello"
cmux browser surface:7 click e2 --snapshot-after
cmux browser surface:7 screenshot --out /tmp/cmux.png
cmux browser surface:7 console list
cmux browser surface:7 errors list
```

If `snapshot --interactive` or `eval` fails, use `get url`, `get text body`, or `get html body` to inspect the page.

## Settings

Before changing cmux settings, run:

```bash
cmux docs settings
cmux settings path
```

Back up the user `cmux.json`, edit cmux-owned settings there, then reload with `cmux reload-config`. Terminal rendering belongs to Ghostty config, not cmux settings.
