Stricepta-Coder gets native roles in the style of Zoo Code modes, one role map for Anthropic and local models, with per-role tools, thinking, sampling and permissions.

# Stricepta-Coder: roles native in the host

The user (2026-11-10): Zoo Code has roles (modes); integrate this in the host. Zoo Code is an inspiration only and does not run alongside Stricepta-Coder; Claude Code is the bigger inspiration.

What Zoo Code does (read 2026-11-10 at `docs.zoocode.dev/features/custom-modes`; the successor of the archived Roo Code): a mode is an entry of `customModes` in `custom_modes.yaml` (global) or `.roomodes` (project, wins over global): `slug`, `name`, `description`, `roleDefinition`, `whenToUse`, `customInstructions`, `groups` (`read`, `edit` with a `fileRegex` restriction, `command`), and rules files in `.roo/rules-<slug>/`. Built-in modes: Code, Debug, Ask, Architect, Orchestrator; a custom mode with a built-in slug overrides it. Switching is a dropdown in the chat input or a `/` command. Per-mode MCP restrictions exist. Not read: how the Orchestrator hands a task to a mode, and whether a mode can pin a model (the pages for those were not checked).

What the harness has: `roles.json` of a dev root (here `.kk_harness/roles.json`, keys `default`, `roles`, `groups`, `fallback_role`; a role has `model`, `description`, `task`, `parameters`, `system_prompt`). A role cannot yet switch thinking or sampling by itself, carry a tool subset or permissions (`harness-per-role-thinking-control` and the tool-subset question in `role-fit`, in the roadmap and knowledge of `AI/claude`).

Ideas, none decided:

- One role definition format for the host that reads both: Zoo Code's fields (`slug`, `roleDefinition`, `whenToUse`, `groups` with file restrictions) plus the harness's model, parameters (thinking, sampling, context) and a local twin for each Anthropic tier, so the usage-limit switch (`stricepta-coder-model-mixing`) swaps the model and keeps the role.
- Whether to read `.roomodes` and `custom_modes.yaml` as an import format is open; the host defines its own format first.
- A mode dropdown in the GUI with the active role, model and endpoint always visible; the orchestrator role as the default entry (`stricepta-coder-routing-and-orchestrator`).
- Rules, hooks and permission sets per role (the reader role gets no write tools); the refusal figures of the model cards decide which model may take story, canon and asset roles.
- Role presets per project profile (`harness-project-profile-orchestrator`).

Ranked after the plugin items. Not built, nothing decided. Delete this item when it is built or dropped.
