Further GUI improvements of Stricepta-Coder (terminal UI, web, extension).

# Stricepta-Coder: GUI improvements

The user (2026-11-10): further GUI improvements, without a list yet. Open: which surfaces count (terminal UI, `web/`, the extension), and what the user wants changed; collect the wishes before any design.

## The wish list (the user, 2026-11-13)

- **Rework the GUI, the chat area and the control center.** The theme looks terrible to the user, and it must be isolated: it may not overwrite the overall theme of Code OSS / VS Code. Source (read 2026-11-13, nothing run): the extension ships a color theme `vscode-extension/openclaude-vscode/themes/OpenClaude-Terminal-Black.json` (contributed through `package.json`; a contributed theme is only active when the user selects it, so the overwrite to check is whether the extension applies it or `workbench.colorCustomizations` on its own: not found in `src/`, to confirm live); the chat webview `src/chat/chatRenderer.js` uses the `--vscode-*` font variables but hard-coded colors otherwise. Direction: the webviews take every color from the `--vscode-*` theme variables and the theme file becomes optional; the control center and the chat share one stylesheet and one component set.
- **An LM Studio-like chat workflow:** subfolders for chats, ordering chats into groups. Source: sessions are listed by `src/chat/sessionManager.js` (class `SessionManager`, reading the transcript folder of the host); a folder or group is metadata beside the transcript (a tag or a group file in the projects folder), never a move of the transcript, so the host's resume keeps working. Groups per project, drag into a group, a default group per dev root.
- **New panels that the other items need and this item designs:** the session settings panel and the control-center pages for presets, roles, toggles, models and VRAM (`stricepta-coder-session-settings`), the setup wizard (`stricepta-coder-setup-wizard`), the session state view (`stricepta-coder-stateful-sessions`).

Order inside this item: the theme isolation first (a defect the user sees in every session), then the shared stylesheet and components (everything after builds on them), then the chat groups, then the new panels as their items are built. The GUI of the extension depends on `stricepta-coder-vscode-extension-repo` for where the code lives, not for what it does.

Ranked after the plugin items (ledger `2026-11-10-stricepta-coder-scope-split-and-ranked-last`). Not built, nothing decided. Delete this item when it is built or dropped.
