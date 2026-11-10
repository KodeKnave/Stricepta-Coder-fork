Stricepta-Coder routes each task in its own window to Anthropic or to a local model, and may run a small local model as orchestrator that delegates most work.

# Stricepta-Coder: routing and a local orchestrator

The user (2026-11-10): Claude Code does not swap models by itself and only moves between Anthropic models, so it cannot hand work to a local model directly, which would take load off the Anthropic models. Stricepta-Coder can route inside its own IDE window to Anthropic or to local models, and may itself have a local model as orchestrator.

Candidate named by the user, a hypothesis to test: MiniCPM5 2B, because it admits when it does not know what to do and so delegates most work anyway. Its card says it is not abliterated and is meant for tool plumbing on code and tool output (`knowledge/models/minicpm5-2b-nvfp4.md` and `role-assignments.md` in the harness library, `AI/claude`). The measured orchestrator comparison of the library (Gemma 4 12B against Qwen3.8 9B) is still open there; add MiniCPM5 to it.

Open: who decides a route (a rule, a hook, the orchestrator's judgment: `harness-task-routing` item 5 in the library roadmap), what the orchestrator sees of the other models' work, and how this works while the Anthropic usage limit is reached (`stricepta-coder-model-switching`).

Ranked after the plugin items. Not built, nothing decided. Delete this item when it is built or dropped.
