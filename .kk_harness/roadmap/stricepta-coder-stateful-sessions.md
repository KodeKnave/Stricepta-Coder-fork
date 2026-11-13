Sessions of Stricepta-Coder become stateful: one session object that lives from start to end and that the host, the extensions and the GUI read and update, instead of state scattered over files.

# Stricepta-Coder: stateful sessions

The user (2026-11-13): sessions become stateful (currently stateless); this could allow more optimizations regarding workflows.

## What is stateless today

The host writes the transcript (`src/utils/sessionStorage.ts`) and keeps a small in-process state (`src/utils/sessionState.ts`); every hook run starts from nothing and reads what it needs from the payload or from files. The harness works around this with its own state: the session keys in `.kk_harness/state/` (what was read, which rules were injected, which nudges were shown, the hold counters), the SQLite telemetry file, the ledger and handoff, and the role files of a subagent call (`.roles/tasks/`). Every hook pays the reads at every event, and two hooks that need the same fact compute it twice.

## Evaluation (2026-11-13, nothing built, nothing run)

- **One session object** (the `SessionState` of `stricepta-coder-extension-api`) with the facts the harness keeps in files today: files read and their line ranges, rules and knowledge injected, the tool calls of the turn, edits since the last test run, the open nudges, the active role and model with its window, the leases of local models. The host owns it, extensions read and update it through the API, the GUI shows it (`stricepta-coder-session-settings`: the session panel).
- **Workflow optimizations this allows:** read de-duplication and the read gates without a key file per session; a Stop check that knows what the turn did without parsing the transcript; a close-check that asks the user once and remembers the answer; subagent calls that carry the parent's state (what is already read) instead of a brief alone; a compaction that rebuilds the state from the object instead of losing the keys (today a compaction wipes several session keys and the gates arm again).
- **Persistence:** the object is saved with the transcript (one JSON next to the `.jsonl`, or a table in the host's SQLite) so a resumed session continues with its state; the harness's `.kk_harness/state/` folder then holds only what spans sessions (the handoff, the ledger, the telemetry).
- **Not a replacement for the ledger and handoff:** those are the record across sessions and stay files in the repo; the session state is the record inside one session.
- **Presets and roles** (`stricepta-coder-session-settings`, `stricepta-coder-roles-native`) are the configuration a session starts with; the session state is what changes while it runs. Keep the two apart: a preset is editable before the start, state is read during the run.

Open: what a resumed session restores and what it recomputes; whether a subagent gets a copy or a view of the parent's state; which state the GUI may change during a run (the open question of `stricepta-coder-session-settings`).

Related: `stricepta-coder-extension-api`, `stricepta-coder-session-settings`, `stricepta-coder-native-harness`, `harness-indexed-memory` in `AI/claude/roadmap/`. Ranked after the plugin items with the other Stricepta-Coder items. Delete this item when it is built or dropped.
