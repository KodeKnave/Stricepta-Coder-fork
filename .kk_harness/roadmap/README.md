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
| 8 | **GUI improvements** (terminal UI, `web/`, extension) | [gui](stricepta-coder-gui.md) | `vscode-extension/openclaude-vscode/src/` | |
| 8a | Rework of the chat area and the control center; the theme isolated, never overwriting the Code OSS / VS Code theme | same | `themes/OpenClaude-Terminal-Black.json`, `src/chat/chatRenderer.js` (hard-coded colors), `src/extension.js` (Control Center) | |
| 8b | LM Studio-like chat workflow: subfolders and groups of chats | same | `src/chat/sessionManager.js` (`SessionManager`) | |
| 8c | The new panels of goals 12 to 14 (session settings, control-center pages, setup wizard, session state) | same | not checked | |
| 9 | **Image generation connection** to SwarmUI or ComfyUI, opt in, built in or CLI, MCP last | [image-generation](stricepta-coder-image-generation.md) | not checked | `harness-image-generation-connection` |
| 10 | **Own LLM backends** in the extension (llama.cpp, mistral.rs, model folders, a dispatcher interface; LM Studio and the Claude Code backend optional) | [llm-backends](stricepta-coder-llm-backends.md) | not checked | `harness-concurrent-local-models` |
| 11 | **Extension API**: the hook events as native code behind typed extension points with the full session state (a Java-interface-like contract, not a marketplace); a built-in extension runs the plugin's shell hooks meanwhile | [extension-api](stricepta-coder-extension-api.md) | `HOOK_EVENTS` in `src/entrypoints/sdk/coreTypes.ts`, `createBaseHookInput` in `src/utils/hooks.ts` | `harness-composable-hook-parts`, `harness-host-aware-hooks` |
| 12 | **Stateful sessions**: one session object for the host, the extensions and the GUI, saved with the transcript; the harness state files become its fields | [stateful-sessions](stricepta-coder-stateful-sessions.md) | `src/utils/sessionState.ts`, `src/utils/sessionStorage.ts` | `harness-indexed-memory` |
| 13 | **Session settings**: LM Studio-like presets per session (sampling, context, thinking), roles selected by the preset, the harness toggles, the VRAM estimate of the whole model set; defaults in the control center | [session-settings](stricepta-coder-session-settings.md) | `src/services/api/claude.ts` (`temperatureOverride`), the extension's Control Center | `harness-model-roles`, `harness-per-role-thinking-control`, `harness-concurrent-local-models`, `harness-style-toggles` |
| 13a | Live change of a preset during a session: next request (sampling, thinking), next turn after a reload (model, window), next event (toggles) | same | not checked | |
| 13b | VRAM estimate in GB for all active roles plus the subagent headroom, red when it does not fit | same | `hooks/roles-load.sh` and `hooks/vramlib.sh` of `AI/claude` (the estimate per model) | `harness-concurrent-local-models` |
| 14 | **Setup wizards** in the control center: workplace and dev root, hardware-aware model recommendations and downloads, the preset by project intention; calls `new-devroot.sh` and `setup.sh` | [setup-wizard](stricepta-coder-setup-wizard.md) | `tools/new-devroot.sh`, `tools/setup.sh`, `knowledge/models/` of `AI/claude` | `harness-project-profile-orchestrator`, `harness-lint-checks` |

Goal 1 is the first part of goal 6; goal 2 builds on the plugin's manual fallback; goals 3 and 4 share one role map. Goals 11 and 12 are the technical basis of goal 6 (added 2026-11-13 with goals 13 and 14); goal 13 selects roles from the map of goal 4 and shows the estimate of goal 10's backends; goal 8 designs the panels of goals 12 to 14.
