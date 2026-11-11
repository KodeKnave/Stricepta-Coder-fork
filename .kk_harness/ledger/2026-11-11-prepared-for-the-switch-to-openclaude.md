## 2026-11-11 — Handoff prepared for work in OpenClaude

The handoff names goal 9 (image generation connection, added today) and says the plugin repo `AI/claude` comes first. Nothing else changed; nothing is built here.

Setup: `setup.sh` ran for this root (the `CLEANUP_DIALOG` toggle), the profile lost its placeholders (`openai`, model `local-model`, window 65536, max output 16384, like the library's), `roles.json` is the template (coder, reader, reviewer; fits a TypeScript code repo). The live checks are in `AI/claude/roadmap/harness-openclaude-fallback-dev-root.md`.
