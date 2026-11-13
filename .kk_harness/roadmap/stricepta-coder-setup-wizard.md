Setup wizards in the control center: set up a workplace and a dev root, and recommend models and settings by the machine's hardware and the project's intention.

# Stricepta-Coder: setup wizards

The user (2026-11-13): add setup wizards (in the control center?) to easily set up a workplace and a dir; recommended model downloads and setup options depending on hardware and project intention, maybe.

## What exists

The harness does the setup from the terminal: `kk-claude-harness new-devroot [--kind code|assets|prose] ... "<dir>"` writes the files of a consumer repo (settings, `CLAUDE.md`, `.kk_harness/` with handoff, roadmap, ledger, knowledge, `config.json`, the OpenClaude profile and settings), `kk-claude-harness setup "<dev root>"` repairs and updates the machine and the roots (plugin install, git hooks, MCP allow rules, OpenClaude links); the README of `AI/claude` ("User guide", sections 1 to 3) describes the steps and `knowledge/dev-setup.md` the machine. Model knowledge: the model cards and role assignments in `AI/claude/knowledge/models/` (which model fits which role, the refusal figures, the GPU of this machine), the VRAM gate's estimate per model and window.

## Evaluation (2026-11-13, nothing built, nothing run)

- **The wizard calls the scripts, it does not replace them.** `new-devroot.sh` and `setup.sh` stay the one implementation (the terminal and Claude Code keep using them); the wizard is a form in the control center that collects the arguments (folder, kind, name, excluded folders, model) and runs the script, showing its output. The `--check` mode gives the wizard its "what is missing" page for an existing root.
- **Hardware:** read the card and its memory (`nvidia-smi`, what `vramlib.sh` reads today), the RAM and the disk, and show what fits: a 27B at a 32k window, a 9B with a 2B reader beside it, and so on, using the same estimate as the VRAM panel of `stricepta-coder-session-settings`.
- **Intention:** the kind of the dev root (`code`, `assets`, `prose`) plus the language or engine (Python, C#, Godot, Blender, a Warband module) decides the preset: the roles to activate, the models the model cards recommend for them, the lint step (`harness-lint-checks`), the Read deny rules for binaries. A project profile (`harness-project-profile-orchestrator`) is the same idea for the orchestrator; keep one profile format for both.
- **Model downloads:** recommended models as a list with size, window and the role they fit, downloaded through the backend (LM Studio today, `lms get`; own backends later, `stricepta-coder-llm-backends`), never bundled. The recommendation comes from the model cards in `knowledge/models/`, so writing a card is how a model enters the wizard.
- **Order of the pages:** machine (hardware, dependencies: `jq`, `perl`, `python3`, `node`, `sqlite3`, the plugins), then workplace (folder, kind, name), then models (what fits, what to download), then the preset (the roles and toggles, editable later in the settings panel), then the run of the scripts with their output.

Open: whether the wizard also creates the git repository and the first commit; how it handles a folder that is already a dev root (repair mode = `setup --check`, then `setup`); whether the recommendations consider the Anthropic subscription (model mixing, `stricepta-coder-model-mixing`).

Related: `stricepta-coder-session-settings`, `stricepta-coder-gui`, `stricepta-coder-llm-backends`; in `AI/claude/roadmap/`: `harness-project-profile-orchestrator`, `harness-lint-checks`, `harness-model-roles`. Ranked after the plugin items with the other Stricepta-Coder items. Delete this item when it is built or dropped.
