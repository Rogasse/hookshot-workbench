---
name: hookshot-context
description: Use for Rogasse's Hookshot gameplay, performance testing, source contributions, or Hookshot GitHub and team-chat coordination; load and maintain the durable Windows workbench context.
---

# Hookshot context for Rogasse

The durable handoff is `~/Documents/Codex/hookshot-workbench` on Rogasse's Windows PC, published at https://github.com/Rogasse/hookshot-workbench. Read its `AGENTS.md`, `docs/CURRENT.md`, and `docs/TASKS.md` before Hookshot work. If the local checkout is unavailable, read those files from the public repository. Check current evidence and linked upstream discussions before acting; these notes may be older than the current release or PR head.

After a meaningful result, update `docs/WORKLOG.md` and the relevant current state or task row. Keep raw game data, saves, binaries, keys, caches, credentials, options, and local paths out of the public repository. Publishing a workbench update or an upstream comment still requires authorization from the user's request or session context; this skill alone grants none. Verify `gh api user --jq .login` returns `Rogasse` immediately before any GitHub write.

For an upstream code contribution, follow Hookshot's current `docs/workflow.md`, `AGENTS.md`, and `CONTRIBUTING.md`. For a performance comparison, use the workbench's `docs/METHOD.md` and report both repeated runs and limits of the evidence. Do not run mooki000's Linux-specific scripts on this Windows PC without adapting and checking them first.
