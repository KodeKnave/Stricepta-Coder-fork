Where Stricepta-Coder stands: the decisions in force and what is next.

# Handoff

What git and the ledger know (branch, uncommitted paths, newest entries) is generated at the session start and is not written here.

## Decisions

- Stricepta-Coder is built after the plugin `harness@kode-knave` is finished; the plugin is the reference base (the user, 2026-11-10). → `ledger/2026-11-10-scope-bigger-picture-and-items-moved-here.md`
- Claude Code does not swap models by itself and switches only between Anthropic models; Stricepta-Coder may route to Anthropic or local models and run a local orchestrator (MiniCPM5 2B is a candidate to test) (the user, 2026-11-10). → same entry
- Zoo Code is an inspiration for the roles of Stricepta-Coder, not a component that runs alongside it; Claude Code is the bigger inspiration (the user, 2026-11-10). → `ledger/2026-11-10-roles-native-item-and-zoo-code-modes.md`
- `CLAUDE.md` of this repo is tracked through `!/CLAUDE.md` in `.gitignore`; keep the line when merging upstream (the user, 2026-11-10). → `ledger/2026-11-10-claude-md-tracked-despite-forks-gitignore.md`

- Stricepta-Coder uses Anthropic and local models simultaneously in one session, the split of tasks configurable; an Anthropic model whose usage limit is used up is out of order until it is restored (the user, 2026-11-10). → `ledger/2026-11-10-model-mixing-is-simultaneous-and-switching.md`

## Next

Nothing is built. The goal and the six work areas: [`knowledge/bigger-picture.md`](knowledge/bigger-picture.md); what the harness learned: [`knowledge/harness-wisdom.md`](knowledge/harness-wisdom.md). All goals and features in one table: [`roadmap/README.md`](roadmap/README.md); open items: [`roadmap/`](roadmap/), starting once the plugin items are done.
