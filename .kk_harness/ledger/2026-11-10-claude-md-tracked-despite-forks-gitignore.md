## 2026-11-10 — CLAUDE.md is tracked; the fork's .gitignore had ignored it

The fork's `.gitignore` ignored `CLAUDE.md` (line 14) and `GEMINI.md` since the OpenClaude upstream: `GEMINI.md` came with a gRPC server PR (#278, 2026-04-06), `CLAUDE.md` with an unrelated tool-result compression PR (#801, 2026-04-21); the reason is not stated in either commit. The dev root index `CLAUDE.md` of this repo was therefore untracked. Added `!/CLAUDE.md` after the line and committed the file (`6e4464a0`). The other ignored paths were looked at: the `.claude/` subfolders and `.kk_harness/state/` are machine-local by our scaffold, `.openclaude/`, `.openclaude-profile.json` and `reports/` are the fork's own (`reports/` not opened).

Decision: `CLAUDE.md` of this repo is tracked through `!/CLAUDE.md` in `.gitignore`; keep the line when merging upstream (the user, 2026-11-10).
