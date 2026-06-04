# coding-agent-common

Reusable coding-agent assets: skills, prompt patterns, review workflows, and small utilities that should stay useful across projects.

This repository starts intentionally small. Add an asset when it captures repeated agent work, preserves a clear principle, or prevents a known failure mode. Keep prompts and skills concise enough that another agent can use them without inheriting stale assumptions.

## Contents

- `skills/prompt-intent`: A Codex skill for writing and reviewing prompt-like instructions with commander-intent framing and a minimum-specification filter.

## Principles

- Treat any instruction surface an agent reads as a prompt, including skills and tool descriptions.
- Start with the agent's execution context: what it will know, what it can see, and what it cannot infer from the prompt-writing conversation.
- Communicate intent, desired end state, relevant context, and real constraints before procedure.
- Keep hard rules for invariants. Use softer guidance for context-dependent heuristics.
- Delete prompt text that is obvious, duplicated, unverifiable, stale, or not tied to a known need.
- Move deterministic enforcement into code, schemas, tests, validators, permissions, or tools when those are the better control surface.

## Installing A Skill

For Codex, copy or symlink a skill folder into your skills directory:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
ln -s "$(pwd)/skills/prompt-intent" "${CODEX_HOME:-$HOME/.codex}/skills/prompt-intent"
```

## Source Notes

This repo's initial prompting principles are informed by:

- [DINFOS, "Commander's Intent Across the Services"](https://pavilion.dinfos.edu/Article/Article/2160695/commanders-intent-across-the-services/): commander intent as concise purpose, end state, context, and autonomy when plans change.
- [Marine Corps Association, "Commander's Intent Defined"](https://www.mca-marines.org/gazette/commanders-intent-defined/): intent should not duplicate the plan and is easier to use when concise.
- [Liberating Structures, "Min Specs"](https://www.liberatingstructures.com/14-min-specs/): keep only the must-do and must-not-do rules needed to achieve a purpose.
- [Plexus Institute Edgeware, "Principles"](https://www.plexusinstitute.com/edgeware/archive/think/main_prin3.html): minimum specifications define no more than necessary to launch action.
- [Red Hat Developer, "Prompt engineering: Big vs. small prompts for AI agents"](https://developers.redhat.com/articles/2026/02/23/prompt-engineering-big-vs-small-prompts-ai-agents): prompt size and structure trade off maintainability, cost, focus, and flexibility.

## License

MIT
