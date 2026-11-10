Stricepta-Coder uses Anthropic and local models together, simultaneously in one session with a configurable split of tasks; an Anthropic model whose usage limit is used up is out of order until it is restored.

# Stricepta-Coder: Anthropic and local models together

The user (2026-11-10): the host supports Claude Code's Anthropic models and local models at the same time, not only by switching. Two modes, both wanted:

1. **Simultaneous use.** Anthropic and local models work in the same session in parallel, each on the tasks the user assigns, so the local models take load off the Anthropic models all the time, not only after the limit. Which model takes which task is configurable (through the roles and the routing rule), not fixed; an Anthropic model that plans and reviews while local models implement is one possible setup, not the design.
2. **Out of order at the usage limit.** An Anthropic model whose usage limit is used up (a model's own limit or the general one) is out of order until the limit is restored; its tasks go to the models still available, local ones included, and it takes them back once restored, repeating. Anthropic models whose limits are not used up stay in use. This is the fallback of `harness-openclaude-fallback` and `harness-openclaude-fallback-dev-root` (roadmap of `AI/claude`) built into the host instead of a manual restart in OpenClaude.

Claude Code does not swap models by itself and only switches between Anthropic models (haiku, sonnet, opus), never to a local one, so it takes work off the Anthropic models only through subagents; Stricepta-Coder can route in its own window to Anthropic or to local models, which would make `harness-task-routing` routes 2 and 3 (swaps and role combos, in the roadmap of `AI/claude`) work in the host without a restart. Who decides a route is the item `stricepta-coder-routing-and-orchestrator`.

Open, each needing a look at the source first: how several model providers run in one session at once (one endpoint per model, concurrency, the VRAM gate for local models that `harness-concurrent-local-models` built for OpenClaude), how the host learns that a model's limit is used up and when it is restored (per model or general), what state (history, handoff, role) carries across a switch, and which local model takes over by the project profile (`harness-project-profile-orchestrator`).

Ranked after the plugin items (`knowledge/bigger-picture.md`). Not built, nothing decided. Delete this item when it is built or dropped.
