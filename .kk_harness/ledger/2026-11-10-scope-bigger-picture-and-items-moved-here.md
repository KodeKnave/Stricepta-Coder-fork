## 2026-11-10 — The host scope, the bigger picture and the work items now live in the Stricepta-Coder repository

The user set the scope of Stricepta-Coder (both model families with automatic switching at the usage limit, the tools and the harness built into the source, the VS Code extension in its own repository, GUI improvements) and asked that the items and the reasoning be kept in this repository. The six roadmap items `stricepta-coder-*` moved here from `AI/claude/roadmap/`, plus a new one, `stricepta-coder-routing-and-orchestrator`. `knowledge/bigger-picture.md` states the goal and `knowledge/harness-wisdom.md` what the harness learned; `CLAUDE.md` points to both.

Decision: Stricepta-Coder is built after the plugin `harness@kode-knave` is finished, which serves as its reference base (the user, 2026-11-10).

Decision: Claude Code does not swap models by itself and only switches between Anthropic models; Stricepta-Coder may route to Anthropic or local models in its own window and may use a local orchestrator, MiniCPM5 2B being a candidate to test (the user, 2026-11-10).
