Features the harness wants from Stricepta-Coder, the user's own OpenClaude fork that is to become a host with extra events; Claude Code stays the main host, so each feature is optional there; the wider host scope is in the items `stricepta-coder-*` (ranked last, after the plugin items).

# Stricepta-Coder as a harness host

The user (2026-11-07): `/home/roman/Arsenal_II/Projekte/AI/Stricepta-Coder` (a fork of OpenClaude at the same commit as `/home/roman/Arsenal_II/Projekte/AI/openclaude`, `cd665547`) becomes a host of its own, something like the harness integrated as an IDE: extra hooks and events (a `PreStop`, say). A plugin comes first; the host is extended only where a plugin cannot do it ("in the worst of the worst cases"). Claude Code has to stay supported, so the harness keeps working without any of these, and Stricepta-Coder is mostly the host where a gap can be closed. Both repos are dev roots of `setup-all` (`HARNESS_UPDATE_ROOTS`).

The list is a start of proposals taken from what the harness worked around so far; each needs a look at the source and a decision before it is built:

- Project files of Claude Code as an opt-in fallback (a setting): `.claude/settings*.json`, `.claude/CLAUDE.md`, the folders `skills`, `commands`, `agents`, `output-styles`, `workflows`. OpenClaude isolates them by design (issue 1875, `harness-openclaude-no-claude-fallback`); the harness mirrors settings keys and links folders to make up for it.
- A `PreStop` event (before the turn ends), and a way for a hook to ask the user itself. Today the Stop block makes the model call `AskUserQuestion` (`close-check`), which a 9B cannot do (ledger `2026-11-06-openclaude-write-ask-live-run-and-nudge-findings`).
- Session permission rules seeded from a settings file or a flag: the write ask under `.openclaude/` and `.claude/` is lifted only by a rule of the session source, and nothing seeds one (`harness-openclaude-write-ask`).
- A refused or unanswerable permission as a hook event, so the harness can make the model stop and ask the user instead of working around it (the wish in `harness-openclaude-write-ask`): the events `PermissionRequest` and `PermissionDenied` already exist (see below); what a refused write ask looks like to them is not checked.
- Harness toggles from a project settings file before the trust dialog, limited to a named prefix or list (`START_*`, `HK_*`); today only an allowlist of safe variables applies before the dialog, the rest after (`src/utils/managedEnv.ts`).
- The real context window in the hook payload, so `HK_CONTEXT_WINDOW` need not be set by hand per model (the status line passes it only through a state file).
- A plugin that may ship `permissions` and `env` defaults: a Claude Code plugin cannot, which is why `setup.sh` writes the MCP allow rules and syncs the settings keys.

## Where each one sits in the source (read 2026-11-07 in `/home/roman/Arsenal_II/Projekte/AI/Stricepta-Coder`, same commit as `openclaude`; nothing run, nothing changed)

- Hook events: `HOOK_EVENTS` in `src/entrypoints/sdk/coreTypes.ts`, 27 of them: `Stop`, `StopFailure`, `PermissionRequest`, `PermissionDenied`, `PostToolUseFailure`, `SessionStart`, `InstructionsLoaded`, `ConfigChange` among them, no `PreStop`. A new event is an entry there plus the place that fires it; the hook input of every event is built in `createBaseHookInput`, `src/utils/hooks.ts:491` (the context window would join it there).
- Session permission rules from a setting: `src/utils/permissions/permissionSetup.ts:1133` builds `alwaysAllowRules: { cliArg: ... }` from `--allowedTools`; a settings key could fill a session-source list at the same place (the write-ask bypass counts only the session source).
- Harness toggles before the trust dialog: `SAFE_ENV_VARS` in `src/utils/managedEnvConstants.ts:136`, applied in `applySafeConfigEnvironmentVariables` (`src/utils/managedEnv.ts`).
- Opt-in `.claude/` fallback: the project settings paths in `getRelativeSettingsFilePathForSource` (`src/utils/settings/settings.ts`, about line 313), the project instruction files in `src/utils/projectInstructions.ts`, the project folders through `PROJECT_CONFIG_DIR_NAMES` of the markdown loader; `src/skills/siblingSkillHomes.ts` already has the pattern of an opt-in sibling home (`claudeCodeSkillsEnabled`, user level only), which a project-level version would extend.
- A plugin shipping `permissions` and `env`: not located in the plugin loader; not checked.

Stricepta-Coder has no harness folder and no `CLAUDE.md` yet (its `AGENTS.md` is the fork's own, and OpenClaude reads `AGENTS.md` first); its own roadmap would live in `.kk_harness/roadmap/`, which `new-devroot.sh` (with `--no-allowlist` for a repo like this) creates. The user decides whether and when it gets one; until then this item stays here.

## Scope added by the user, 2026-11-10

- Both model families at once: Anthropic models until the usage limit is reached, then local models, and back to Anthropic once the limit is restored, repeating. This is the fallback of `harness-openclaude-fallback` and `harness-openclaude-fallback-dev-root` made automatic inside the host.
- The tools of the harness integrated into the Stricepta-Coder source, as CLIs or fully into the code where that applies, not as MCP servers (like the CBM binaries): 1. CBM, 2. the context-mode plugin, 3. Ponytail, 4. caveman, 5. Headroom, 6. further plugins that fit.
- The VS Code extension leaves the Stricepta-Coder folder (`vscode-extension/`) and becomes a repository of its own.
- Further GUI improvements.
- Every feature, workflow, hook and rule of this harness plugin native in the Stricepta-Coder source.

Open: the order inside this scope, which tool is a CLI and which part of the source, and the repository split; each needs a look at the source first. Stricepta-Coder has a harness folder now (`.kk_harness/` with a `roadmap/`, checked 2026-11-10), which meets the condition for moving this item into its roadmap; it stays here while the order is ranked in this library.

Not built, nothing decided. Delete this item when it has moved into the Stricepta-Coder roadmap, or the list is built or dropped.

Added 2026-11-12: cut a repetition loop inside one generation (a repeated n-gram in the streamed thinking or reply) and treat it as a failed call; the plugin cannot do this, hooks run between tool calls. Reason and the library side: `AI/claude/roadmap/harness-task-routing.md` ("Loops inside a stage").
