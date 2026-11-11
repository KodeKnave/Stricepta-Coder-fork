A built-in connection to SwarmUI or ComfyUI for image generation, opt in, as a CLI or module of the host rather than an MCP server where that works.

# Stricepta-Coder: image generation connection

The user (2026-11-11): a SwarmUI or ComfyUI connection workflow for game development, maybe through MCP, maybe opt in. The library side (the plugin requirement, the toggle, the setup) is `harness-image-generation-connection` in the roadmap of `AI/claude`.

MCP servers exist for ComfyUI (many; list in `harness-image-generation-connection`) and one text-to-image prototype for SwarmUI (web search 2026-11-11, nothing opened). Open, each needing a look first: which backend (SwarmUI API or ComfyUI workflow JSON over HTTP and WebSocket); CLI, host module or MCP server (preference per `stricepta-coder-tool-integration`: MCP last); workflows as saved JSON the model fills, not graphs it builds; output only into the project's write roots.

Why the point exists (the user, 2026-11-11): another AI said SwarmUI and ComfyUI can be controlled through MCP, which is useful for game development (assets, textures, concept art). Read from the three repository READMEs on 2026-11-11 (code, commit dates and activity not read), the shapes a connection takes; the three are alternatives, not one config:

```json
{"mcpServers": {
  "comfyui-artokun":  {"command": "npx", "args": ["-y", "comfyui-mcp"], "env": {"COMFYUI_HOST": "127.0.0.1", "COMFYUI_PORT": "8188"}},
  "comfyui-miller":   {"command": "npx", "args": ["-y", "@miller-joe/comfyui-mcp", "--stdio", "--comfyui-url", "http://127.0.0.1:8188"]},
  "comfyui-joenorton": {"type": "streamable-http", "url": "http://127.0.0.1:9000/mcp"}
}}
```

- `artokun/comfyui-mcp` (MIT, npm, TypeScript): stdio through `npx`; `COMFYUI_HOST` and `COMFYUI_PORT` as above (the port is auto-detected over 8188 and 8000 when unset), or `COMFYUI_URL` for a remote ComfyUI; it can find or download checkpoints and builds the workflow itself, with an optional panel, skills and hooks of its own (a second harness layer to weigh).
- `miller-joe/comfyui-mcp` (MIT, npm): streamable HTTP by default on port 9100, `--stdio` for stdio clients; `--comfyui-url` or `COMFYUI_URL`, default `http://127.0.0.1:8188`; text-to-image, img2img, upscale, ControlNet, IP-Adapter, workflow templates.
- `joenorton/comfyui-mcp-server` (Apache-2.0, Python): started by hand with `python server.py` while ComfyUI runs on 8188; workflow JSON files in its `workflows/` folder with `PARAM_*` placeholders become tools (the saved-workflow shape this item wants), and it has `generate_image`, `view_image`, `regenerate`, `list_assets` and `publish_asset` (copies an asset into a project folder and a manifest, useful for a game's asset folder). The client entry goes in a project `.mcp.json`; both `streamable-http` and `http` are accepted as type.
- SwarmUI: only a prototype, `MathewTomberlin/SwarmUI_MCP_Agent` (MIT, text-to-image through two endpoints); not read.
- The ComfyUI Desktop app listens on port 8000, the command line on 8188 (from the artokun README).

For Stricepta-Coder this is the MCP last resort; the built-in alternative is a CLI or module that speaks the ComfyUI HTTP API itself.

Ranked after the plugin items (ledger `2026-11-10-stricepta-coder-scope-split-and-ranked-last`). Not built, nothing decided. Delete this item when it is built or dropped.
