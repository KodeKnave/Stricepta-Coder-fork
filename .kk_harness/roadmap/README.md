The overview of every goal and feature of Stricepta-Coder, one table, with the roadmap file, the source place and the status of each; read it to see all open work at once.

# Roadmap of Stricepta-Coder

One file per item in this folder; this table lists every goal and every feature inside the items. The reasoning behind the goals: [`../knowledge/bigger-picture.md`](../knowledge/bigger-picture.md). All items are ranked after the plugin `harness@kode-knave` is finished (the user, 2026-11-10); the plugin items are in `AI/claude/roadmap/` (named `harness-*` below). Nothing is built, nothing is decided beyond what the item files say. Source places were read on 2026-11-07 in this repo (nothing run); "not checked" means no one looked.

## Goals and features

| # | Goal / feature | Item file | Where in the source | Related plugin item |
|---|---|---|---|---|
| 1 | **Host gaps a plugin cannot close** | [host-features](stricepta-coder-host-features.md) | | |
| 1a | Opt-in `.claude/` fallback (settings, `CLAUDE.md`, skills, commands, agents, output-styles, workflows) | same | `src/utils/settings/settings.ts` (~313), `src/utils/projectInstructions.ts`, `PROJECT_CONFIG_DIR_NAMES`, pattern in `src/skills/siblingSkillHomes.ts` | `harness-openclaude-no-claude-fallback` |
| 1b | `PreStop` event (before the turn ends) and a hook that asks the user itself | same | `HOOK_EVENTS` in `src/entrypoints/sdk/coreTypes.ts` (27 events, no `PreStop`) | `harness-openclaude-write-ask` |
| 1c | Session permission rules seeded from a settings file or flag | same | `src/utils/permissions/permissionSetup.ts:1133` | `harness-openclaude-write-ask` |
| 1d | A refused or unanswerable permission as a hook event | same | `PermissionRequest`, `PermissionDenied` exist; what a refused write ask looks like to them: not checked | `harness-openclaude-write-ask` |
| 1e | Harness toggles from a project settings file before the trust dialog | same | `SAFE_ENV_VARS` in `src/utils/managedEnvConstants.ts:136`, `src/utils/managedEnv.ts` | |
| 1f | The real context window in the hook payload | same | `createBaseHookInput`, `src/utils/hooks.ts:491` | |
| 1g | A plugin that ships `permissions` and `env` defaults | same | plugin loader: not located | |
| 2 | **Anthropic and local models together**: simultaneously in one session (task split configurable); a model whose usage limit is used up is out of order until restored | [model-mixing](stricepta-coder-model-mixing.md) | not checked | `harness-openclaude-fallback`, `harness-openclaude-fallback-dev-root` |
| 3 | **Routing and a local orchestrator** (HIGHLIGHT: the two-stage triage cascade): each task to Anthropic or a local model; MiniCPM5 2B as candidate to test | [routing-and-orchestrator](stricepta-coder-routing-and-orchestrator.md) | not checked | `harness-task-routing`, `harness-project-profile-orchestrator` |
| 4 | **Roles native**, in the style of Zoo Code modes (inspiration only), one role map for both model families, per-role tools, thinking, sampling, permissions | [roles-native](stricepta-coder-roles-native.md) | not checked | `harness-model-roles`, `harness-per-role-thinking-control` |
| 5 | **Tools built in**, as CLIs or code, not MCP servers: CBM, context-mode, Ponytail, caveman, Headroom, further plugins | [tool-integration](stricepta-coder-tool-integration.md) | not checked | |
| 6 | **The harness native**: every feature, workflow, hook and rule of the plugin | [native-harness](stricepta-coder-native-harness.md) | not checked | `harness-composable-hook-parts` |
| 7 | **VS Code extension** in a repository of its own (proposed, not decided) | [vscode-extension-repo](stricepta-coder-vscode-extension-repo.md) | `vscode-extension/` | |
| 8 | **GUI improvements** (terminal UI, `web/`, extension; wish list still empty) | [gui](stricepta-coder-gui.md) | not checked | |
| 9 | **Image generation connection** to SwarmUI or ComfyUI, opt in, built in or CLI, MCP last | [image-generation](stricepta-coder-image-generation.md) | not checked | `harness-image-generation-connection` |
| 10 | **Own LLM backends** in the extension (llama.cpp, mistral.rs, model folders, a dispatcher interface; LM Studio and the Claude Code backend optional) | [llm-backends](stricepta-coder-llm-backends.md) | not checked | `harness-concurrent-local-models` |

Goal 1 is the first part of goal 6; goal 2 builds on the plugin's manual fallback; goals 3 and 4 share one role map.
