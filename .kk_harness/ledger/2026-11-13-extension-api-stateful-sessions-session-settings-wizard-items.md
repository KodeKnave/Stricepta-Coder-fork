## 2026-11-13 — Four roadmap items from the user's new points: extension API, stateful sessions, session settings, setup wizards; the GUI wish list

The user (in a session at `AI/claude`, run on Fable 5.1) gave eight new points for Stricepta-Coder and asked for an evaluation, roadmap items and rows in `roadmap/README.md`. Written, nothing built or run:

- `roadmap/stricepta-coder-extension-api.md` (goal 11): the hook events become native code behind typed extension points that receive the full session state, a contract like a Java interface; a built-in extension runs the plugin's shell hooks unchanged meanwhile. Evaluation: the contract is the first deliverable, the compatibility layer keeps Claude Code and this host on one plugin, third-party extensions are the user's decision.
- `roadmap/stricepta-coder-stateful-sessions.md` (goal 12): one session object instead of the harness's state files, saved with the transcript; the workflow optimizations it allows (gates without key files, a Stop check that knows the turn, subagents that carry the parent's state, a compaction that keeps the state).
- `roadmap/stricepta-coder-session-settings.md` (goal 13, three of the user's points in one place): LM Studio-like presets per session, the roles selected by a preset (the role map stays one, `stricepta-coder-roles-native`), the harness toggles in a panel, the VRAM estimate of the whole model set with subagent headroom. Evaluation of the open question: a preset is editable during a session in three classes (next request, next turn after a reload, next event).
- `roadmap/stricepta-coder-setup-wizard.md` (goal 14): wizards in the control center that call `new-devroot.sh` and `setup.sh`, with hardware-aware model recommendations from the model cards and a preset by project intention.
- `roadmap/stricepta-coder-gui.md` got the wish list: the chat area and control center rework with the theme isolated from the Code OSS / VS Code theme (source read: a contributed theme file, hard-coded colors in `src/chat/chatRenderer.js`), chat subfolders and groups (`src/chat/sessionManager.js`), and the panels the new items need.
- `roadmap/README.md`: rows 8a to 8c, 11 to 14, 13a and 13b, the footer line; `knowledge/bigger-picture.md` lists goals 7 to 10 now; `HANDOFF.md` says fourteen goals.

Decision: a session preset selects and overrides roles from the one role map; the map holds the definitions, never the preset (Claude, 2026-11-13, for the user to correct).

Not committed: the user commits.
