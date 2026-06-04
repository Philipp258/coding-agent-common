# coding-agent-common

Small reusable assets for coding agents.

Start narrow. Add only things that are useful across projects and worth maintaining.

## Contents

- `skills/cmux`: Use cmux topology, terminal surfaces, and browser automation.
- `skills/prompt-intent`: Write and review minimal agent prompts.

## Install

For Codex, copy or symlink a skill folder into your skills directory:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
ln -s "$(pwd)/skills/prompt-intent" "${CODEX_HOME:-$HOME/.codex}/skills/prompt-intent"
```
