Stricepta-Coder runs its own LLM backends (llama.cpp, mistral.rs) behind a dispatcher interface, so LM Studio is no longer needed.

# Stricepta-Coder: own LLM backends

The user (2026-11-12): provide LLM backends in the IDE extension directly, which makes LM Studio obsolete: llama.cpp, mistral.rs, model folder setups, a dispatcher interface. It could become a real product, with the Claude Code backend optional.

Evaluation (2026-11-12, nothing run or checked in the source):
- Clean order: the dispatcher interface first. llama.cpp's server, mistral.rs and LM Studio all speak an OpenAI-compatible HTTP API, so one adapter covers all three; a bundled backend is then one more adapter, and Claude Code / Anthropic is one more. Bundling a backend before the interface would hard-wire it.
- What LM Studio does for the harness today and Stricepta would own: model download and listing, load and unload with a context length, the VRAM estimate (`lms load --estimate-only`, used by the library's VRAM gate) and the lease logic of `harness-concurrent-local-models`. llama.cpp has no estimate command of the same kind; mistral.rs: not checked. This is the main cost.
- Model folders: a setting that lists folders scanned for GGUF files (and mistral.rs formats), with a role map pointing at files, shares the role map of `stricepta-coder-roles-native`.
- Build and GPU backends (CUDA, Vulkan) per platform are the maintenance burden: ship the server binaries as a download step, not in the repo.
- Product angle: a Claude-free mode needs the host's Anthropic assumptions removed (`stricepta-coder-native-harness`); keep it a later step.

Related: `stricepta-coder-model-mixing`, `stricepta-coder-roles-native`, `stricepta-coder-vscode-extension-repo`. Ranked last with the other Stricepta items. Delete this item when it is built or dropped.
