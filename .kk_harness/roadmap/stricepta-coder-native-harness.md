Every feature, workflow, hook and rule of the harness plugin becomes native in the Stricepta-Coder source, with the finished plugin as the reference.

# Stricepta-Coder: the harness native in the host

The user (2026-11-10): all features, workflows, hooks and rules of this plugin natively in the Stricepta-Coder source. The plugin is built to the end first (the user, 2026-11-10) and serves as the reference base. `stricepta-coder-host-features` lists the gaps a plugin cannot close (events, permission seeding, `.claude/` fallback) and is the first part of this work.

Open: which hooks become events or code of the host and which stay scripts, how Claude Code keeps working from the same plugin, and where the shared rules and knowledge live so the two do not drift apart.

Added 2026-11-13 (the user): the technical basis is an extension API with typed extension points and the full session state (`stricepta-coder-extension-api`), with stateful sessions (`stricepta-coder-stateful-sessions`); a built-in extension runs the plugin's shell hooks unchanged, so Claude Code and this host share the plugin while the native parts are built one by one.

Not built, nothing decided. Delete this item when it is built or dropped.
