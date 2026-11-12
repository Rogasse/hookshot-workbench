# Working on Hookshot for Rogasse

Read `README.md`, `docs/CURRENT.md`, `docs/TASKS.md`, and the newest entry in `docs/WORKLOG.md` before starting. This repository is the handoff point between sessions. Update those files after a meaningful result; record dates, pinned versions, commands, evidence, and remaining work. Distinguish observation, inference, and a measured before/after result.

Before working in upstream Hookshot, read its current `docs/workflow.md`, `AGENTS.md`, `CONTRIBUTING.md`, and development guide. Upstream rules take precedence for source contributions. Search existing issues and PRs before starting a fix. Run the relevant source check and full test suite before a PR; a performance claim also needs repeated same-scene runs on the game.

## Identity and public posts

- GitHub publications must come from `Rogasse`. Check the active identity with `gh api user --jq .login` immediately before writing. Stop if it differs.
- The Hookshot team chat account is `@rogasse:magicbean.dev`, accessed through Discord. GitHub and team chat are separate sessions. A saved chat login does not authorize automatic posting.
- Use plain English for upstream reports. State what was measured and what was not. Never claim that a switch or PR improves FPS from a single run or from the player's baseline log alone.

## Data boundaries

- Never commit or upload game content, dumps, `romfs`, `exefs`, saves, generated game code, built executables or DLLs, shader/pipeline caches, keys, credentials, or files copied from another player's game.
- Keep raw run logs, options, screenshots, generated files, local paths, and temporary build output outside this repository. Hookshot permits logs and screenshots in reports when relevant, but inspect them before sharing.
- Check `git status --short` and the staged file list before every commit. Run `git diff --cached --check`.

## Measurement

Use [docs/METHOD.md](docs/METHOD.md). Pin source versions, binary hashes, settings, driver, scene, and cache state. Warm each arm; compare A-B-A-B in the same scene with a quiet PC. Report each run and the spread, plus failures and rejected runs. Preserve the original game binary when testing a renderer variant.

This repository's instructions are for Rogasse's Windows machine. The linked mooki workbench is a methodological reference, not a set of commands to run here.
