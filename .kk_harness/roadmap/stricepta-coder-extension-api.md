The hook events of the harness become native code of Stricepta-Coder, behind an extension API: typed extension points with the full session state, a contract like a Java interface, not a marketplace.

# Stricepta-Coder: hook events as native code behind an extension API

The user (2026-11-13): the current `kk-claude-harness` hook events (`SessionStart`, `Stop` and the others) become native parts of the code. For that, an extension system (not like Claude Code's marketplaces) that allows injecting code at defined points and gives the extension the full session state; think of Java interfaces or abstract classes.

## What it replaces

Today a hook is a shell process per event: it gets a JSON payload on stdin (`createBaseHookInput`, `src/utils/hooks.ts`: `session_id`, `transcript_path`, `cwd`, `permission_mode`, `agent_id`, `agent_type`, plus the event's fields), has no memory between calls (the harness keeps state in `.kk_harness/state/` files and a SQLite file; `handoff/7-hook-state-and-telemetry.md` of `AI/claude` is the contract) and answers with an exit code and text. The 27 events are the list `HOOK_EVENTS` in `src/entrypoints/sdk/coreTypes.ts`; the gaps the harness ran into (no `PreStop`, no way for a hook to ask the user, no context window in the payload) are items 1b to 1g of `stricepta-coder-host-features`.

## Evaluation (2026-11-13, nothing built, nothing run)

- **The contract is the first deliverable.** One TypeScript interface per extension point (`onSessionStart`, `onPreToolUse`, `onStop`, ...) with typed input and a typed answer (allow, block with a reason, inject text, ask the user), and one `SessionState` object every point receives: the transcript so far, the context size and window, the model and role, the loaded instructions and rules, the project folders, the harness state. An abstract base class with no-op defaults means an extension implements only the points it needs. Defining the points as a list plus a dispatcher at each call site keeps the event list the one source of truth, as `HOOK_EVENTS` is now.
- **Compatibility layer, not a rewrite.** The existing shell hooks of the plugin stay valid: one built-in extension runs them as today (payload on stdin, exit code back). So Claude Code and Stricepta-Coder keep running the same plugin while the native parts are built one by one (`stricepta-coder-native-harness`), and a hook that has become native is removed from the plugin's `hooks.json` only for this host (`harness-host-aware-hooks` in `AI/claude`).
- **Why not Claude Code's plugin model:** a marketplace plugin ships files (hooks, skills, commands) and still talks through processes and text; it cannot see the session state or change the host's behaviour between events. The extension API is the layer under it.
- **Stateful by nature:** an extension object lives for the session, so the state files of the harness hooks become fields; this is the technical basis of `stricepta-coder-stateful-sessions`.
- **Loading:** extensions are TypeScript modules, found in a project folder and a user folder (as `.claude/` and `~/.claude/` hold the project and user files today), loaded at start; a failing extension is reported and skipped, never a crash of the host. Whether a third party may ship an extension (code that runs in the host process) is a decision of the user: the first version loads only the harness's own.
- **Telemetry stays:** the hook telemetry of `hk-run.sh` (outcome, time, context size per hook run) becomes a wrapper of the dispatcher, so `hook-report.sh` keeps its data source.

Open: the list of extension points (start from `HOOK_EVENTS` plus the gaps of `stricepta-coder-host-features`: `PreStop`, a refused permission, the context window); which fields `SessionState` exposes read-only and which writable; whether an extension may call the model itself (a judge role) or only steer the session.

Related: `stricepta-coder-native-harness` (this item is its technical basis), `stricepta-coder-host-features` (the gaps that become extension points), `stricepta-coder-stateful-sessions`, `harness-composable-hook-parts` and `harness-host-aware-hooks` in `AI/claude/roadmap/`. Ranked after the plugin items with the other Stricepta-Coder items. Delete this item when it is built or dropped.
