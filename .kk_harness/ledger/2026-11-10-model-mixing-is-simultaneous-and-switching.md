## 2026-11-10 — Anthropic and local models are used simultaneously as well as switched

The user corrected goal 2: it is not switching only; both model families are to work at the same time in one session. The item `stricepta-coder-model-switching` is renamed `stricepta-coder-model-mixing` and now names both modes; the roadmap table and the bigger picture say the same. Earlier ledger entries still name the old item name (history, not rewritten). Nothing built.

The user added: which model takes which task is configurable, not fixed; an Anthropic model whose usage limit is used up is out of order until the limit is restored.

Decision: Stricepta-Coder uses Anthropic and local models simultaneously in one session, the split of tasks configurable; an Anthropic model whose usage limit is used up is out of order until it is restored (the user, 2026-11-10).
