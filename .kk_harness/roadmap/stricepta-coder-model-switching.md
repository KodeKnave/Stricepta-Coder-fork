Stricepta-Coder uses Anthropic models until the usage limit is reached, switches to local models, and back to Anthropic once the limit is restored, repeating, inside one session.

# Stricepta-Coder: Anthropic and local models in one session

The user (2026-11-10): the host supports Claude Code's Anthropic models and local models at the same time, with the switch made by the host itself. This is the fallback of `harness-openclaude-fallback` and `harness-openclaude-fallback-dev-root` built into the host instead of a manual restart in OpenClaude.

Open, each needing a look at the source first: how the host learns that the limit is reached and when it is restored, what state (history, handoff, role) carries across a switch, and which local model takes over by the project profile (`harness-project-profile-orchestrator`).

Also open (the user, 2026-11-10): Claude Code does not swap its model by itself and only switches between Anthropic models (haiku, sonnet, opus), never to a local one, so it can take work off the Anthropic models only through subagents; Stricepta-Coder can route in its own window to Anthropic or to local models, which would make `harness-task-routing` routes 2 and 3 (swaps and role combos, in the roadmap of `AI/claude`) work in the host without a restart. The orchestrator question is the item `stricepta-coder-routing-and-orchestrator`.

Ranked after the plugin items (`knowledge/bigger-picture.md`). Not built, nothing decided. Delete this item when it is built or dropped.
