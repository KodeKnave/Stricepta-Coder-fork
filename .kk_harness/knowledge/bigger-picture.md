The goal of Stricepta-Coder and how its work items fit together; read it before planning any host feature.

# Stricepta-Coder: the bigger picture

Stricepta-Coder is the user's fork of OpenClaude (same commit as `AI/openclaude`, `cd665547` at the fork). It is to become the user's own coding host, something like the harness integrated as an IDE (the user, 2026-11-07 and 2026-11-10). Claude Code stays supported and stays the main host while the plugin `harness@kode-knave` (repo `AI/claude`) is built to the end; the finished plugin is the reference base for the host work, so the host items are ranked after the plugin items.

## What the host is to do

1. **Both model families together**: used simultaneously in one session with a configurable split of tasks; an Anthropic model whose usage limit is used up is out of order until it is restored (`stricepta-coder-model-mixing`).
2. **Routing and orchestrator**: route a task in its own window to Anthropic or to a local model; a local model, possibly MiniCPM5 2B, may orchestrate (`stricepta-coder-routing-and-orchestrator`).
2b. **Roles native**, in the style of Zoo Code modes, on one role map for Anthropic and local models (`stricepta-coder-roles-native`).
3. **Tools built in**: CBM, context-mode, Ponytail, caveman, Headroom and further plugins as CLIs or code in the source, not MCP servers (`stricepta-coder-tool-integration`).
4. **The harness native**: features, workflows, hooks and rules of the plugin in the source (`stricepta-coder-native-harness`; the first part is the list of host gaps in `stricepta-coder-host-features`).
5. **The VS Code extension** (`vscode-extension/`) as a repository of its own (`stricepta-coder-vscode-extension-repo`).
6. **GUI improvements** (`stricepta-coder-gui`).

## Where things live

- The work items of the host: `.kk_harness/roadmap/` here. The plugin items they refer to (`harness-task-routing`, `harness-openclaude-fallback`, `harness-model-roles`) are in `AI/claude/roadmap/`.
- What the harness learned about hosts, models and guards: [`harness-wisdom.md`](harness-wisdom.md).
- `README.md`, `AGENTS.md` and `PLAYBOOK.md` are the fork's own OpenClaude files; they describe OpenClaude and are not rewritten for this picture.
